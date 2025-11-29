Investigation Steps / Questions:


✅ SQL queries for each investigation step

1.1 Identify where and when the crime happened

Query:

SELECT evidence_id,
       room,
       description,
       found_time
FROM   evidence
WHERE  TRUNC(found_time) = DATE '2025-10-15'
ORDER  BY found_time;

1.2 Query:

SELECT room,
       COUNT(*) AS evidence_count
FROM   evidence
WHERE  TRUNC(found_time) = DATE '2025-10-15'
GROUP  BY room
ORDER  BY evidence_count DESC;

1.3 Query:

SELECT room,
       MIN(found_time) AS earliest_evidence_time
FROM   evidence
WHERE  TRUNC(found_time) = DATE '2025-10-15'
GROUP  BY room
ORDER  BY earliest_evidence_time;

2. Analyze who accessed critical areas at the time

Query:

SELECT kl.log_id,
       kl.employee_id,
       e.name,
       e.department,
       e.role,
       kl.room,
       kl.entry_time,
       kl.exit_time
FROM   keycard_logs kl
JOIN   employees e
       ON kl.employee_id = e.employee_id
WHERE  kl.room = 'CEO Office'
  AND  kl.entry_time BETWEEN
          TIMESTAMP '2025-10-15 20:30:00'
      AND TIMESTAMP '2025-10-15 21:10:00'
ORDER  BY kl.entry_time;

3. Cross-check alibis with actual logs

3.1 Query:

SELECT a.alibi_id,
       a.employee_id,
       e.name,
       a.claimed_location,
       a.claim_time
FROM   alibis a
JOIN   employees e
       ON a.employee_id = e.employee_id
WHERE  a.claim_time BETWEEN
          TIMESTAMP '2025-10-15 20:30:00'
      AND TIMESTAMP '2025-10-15 21:10:00'
ORDER  BY a.claim_time;

3.2 Quer:

SELECT DISTINCT
       a.alibi_id,
       a.employee_id,
       e.name,
       a.claimed_location,
       a.claim_time,
       kl.room          AS actual_room,
       kl.entry_time
FROM   alibis a
JOIN   employees e
       ON a.employee_id = e.employee_id
JOIN   keycard_logs kl
       ON kl.employee_id = a.employee_id
      AND a.claim_time BETWEEN kl.entry_time
                           AND NVL(kl.exit_time,
                                   kl.entry_time + INTERVAL '10' MINUTE)
WHERE  a.claimed_location <> kl.room
ORDER  BY a.claim_time;

4. Investigate suspicious calls made around the time

Query:

SELECT c.call_id,
       c.call_time,
       c.duration_sec,
       c.caller_id,
       e1.name AS caller_name,
       c.receiver_id,
       e2.name AS receiver_name
FROM   calls c
JOIN   employees e1
       ON c.caller_id = e1.employee_id
JOIN   employees e2
       ON c.receiver_id = e2.employee_id
WHERE  c.call_time BETWEEN
          TIMESTAMP '2025-10-15 20:50:00'
      AND TIMESTAMP '2025-10-15 21:00:00'
ORDER  BY c.call_time;

5. Match evidence with movements and claims

5.1 Query:

SELECT ev.evidence_id,
       ev.room           AS evidence_room,
       ev.description,
       ev.found_time,
       kl.employee_id,
       e.name,
       kl.entry_time,
       kl.exit_time
FROM   evidence ev
JOIN   keycard_logs kl
       ON kl.room = ev.room
      AND ev.found_time BETWEEN kl.entry_time
                           AND NVL(kl.exit_time,
                                   kl.entry_time + INTERVAL '30' MINUTE)
JOIN   employees e
       ON kl.employee_id = e.employee_id
WHERE  TRUNC(ev.found_time) = DATE '2025-10-15'
ORDER  BY ev.found_time, kl.entry_time;

5.2 Query

SELECT DISTINCT
       evi.evidence_id,
       evi.room          AS evidence_room,
       evi.description,
       evi.found_time,
       emp.employee_id,
       emp.name,
       ali.claimed_location,
       ali.claim_time,
       kl.room           AS actual_room,
       kl.entry_time
FROM   evidence evi
JOIN   keycard_logs kl
       ON kl.room = evi.room
      AND evi.found_time BETWEEN kl.entry_time
                           AND NVL(kl.exit_time,
                                   kl.entry_time + INTERVAL '30' MINUTE)
JOIN   employees emp
       ON emp.employee_id = kl.employee_id
LEFT JOIN alibis ali
       ON ali.employee_id = emp.employee_id
      AND ali.claim_time BETWEEN
             TIMESTAMP '2025-10-15 20:30:00'
         AND TIMESTAMP '2025-10-15 21:10:00'
WHERE  TRUNC(evi.found_time) = DATE '2025-10-15'
  AND (ali.claimed_location IS NULL
       OR ali.claimed_location <> kl.room)
ORDER  BY evi.found_time;

6. Combine all findings to identify the killer

6.1 Query:

SELECT DISTINCT kl.employee_id
FROM   keycard_logs kl
WHERE  kl.room = 'CEO Office'
  AND  kl.entry_time BETWEEN
          TIMESTAMP '2025-10-15 20:30:00'
      AND TIMESTAMP '2025-10-15 21:10:00';

6.2 Query:

SELECT DISTINCT a.employee_id
FROM   alibis a
JOIN   keycard_logs kl
       ON kl.employee_id = a.employee_id
      AND a.claim_time BETWEEN kl.entry_time
                           AND NVL(kl.exit_time,
                                   kl.entry_time + INTERVAL '10' MINUTE)
WHERE  a.claimed_location <> kl.room;

6.3 Query:

SELECT DISTINCT caller_id AS employee_id
FROM   calls
WHERE  call_time BETWEEN
          TIMESTAMP '2025-10-15 20:50:00'
      AND TIMESTAMP '2025-10-15 21:00:00'
UNION
SELECT DISTINCT receiver_id AS employee_id
FROM   calls
WHERE  call_time BETWEEN
          TIMESTAMP '2025-10-15 20:50:00'
      AND TIMESTAMP '2025-10-15 21:00:00';

6.4 Query:

SELECT emp.employee_id,
       emp.name,
       emp.department,
       emp.role
FROM   employees emp
WHERE  emp.employee_id IN (
           (SELECT DISTINCT kl.employee_id
            FROM   keycard_logs kl
            WHERE  kl.room = 'CEO Office'
              AND  kl.entry_time BETWEEN
                      TIMESTAMP '2025-10-15 20:30:00'
                  AND TIMESTAMP '2025-10-15 21:10:00')
           INTERSECT
           (SELECT DISTINCT a.employee_id
            FROM   alibis a
            JOIN   keycard_logs kl
                   ON kl.employee_id = a.employee_id
                  AND a.claim_time BETWEEN kl.entry_time
                                       AND NVL(kl.exit_time,
                                               kl.entry_time + INTERVAL '10' MINUTE)
            WHERE  a.claimed_location <> kl.room)
           INTERSECT
           (SELECT employee_id
            FROM (
                SELECT caller_id AS employee_id,
                       call_time
                FROM   calls
                UNION ALL
                SELECT receiver_id AS employee_id,
                       call_time
                FROM   calls
            )
            WHERE  call_time BETWEEN
                      TIMESTAMP '2025-10-15 20:50:00'
                  AND TIMESTAMP '2025-10-15 21:00:00')
       );

📝 A final “Case Solved” query that reveals the killer in below single column table format:

SELECT emp.name AS killer
FROM   employees emp
WHERE  emp.employee_id IN (
           (SELECT DISTINCT kl.employee_id
            FROM   keycard_logs kl
            WHERE  kl.room = 'CEO Office'
              AND  kl.entry_time BETWEEN
                      TIMESTAMP '2025-10-15 20:30:00'
                  AND TIMESTAMP '2025-10-15 21:10:00')
           INTERSECT
           (SELECT DISTINCT a.employee_id
            FROM   alibis a
            JOIN   keycard_logs kl
                   ON kl.employee_id = a.employee_id
                  AND a.claim_time BETWEEN kl.entry_time
                                       AND NVL(kl.exit_time,
                                               kl.entry_time + INTERVAL '10' MINUTE)
            WHERE  a.claimed_location <> kl.room)
           INTERSECT
           (SELECT employee_id
            FROM (
                SELECT caller_id AS employee_id,
                       call_time
                FROM   calls
                UNION ALL
                SELECT receiver_id AS employee_id,
                       call_time
                FROM   calls
            )
            WHERE  call_time BETWEEN
                      TIMESTAMP '2025-10-15 20:50:00'
                  AND TIMESTAMP '2025-10-15 21:00:00')
       );

Output:

<img width="1104" height="874" alt="image" src="https://github.com/user-attachments/assets/0ced509c-90d8-4a3e-8bcf-8aa5c9fc9f6c" />

🕒 A short explanation of how you arrived at the conclusion

Evidence (evidence) is used to determine the crime date, main room, and approximate time of the murder.

Access logs (keycard_logs) show who entered the CEO Office around that time.

Alibis (alibis) are compared with actual access logs to find employees whose claimed location doesn’t match their keycard movements.

Call records (calls) identify people making or receiving calls around 20:50–21:00, close to the murder time.

Using INTERSECT, we find the single employee who:

Was in the CEO Office during the crime window,

Lied about their location (false alibi),

And was involved in calls around the critical time.

That employee’s name from employees.name is returned as the killer.
