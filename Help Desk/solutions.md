# Helpdesk
![hd](https://github.com/user-attachments/assets/93f2236d-4334-49e9-ad29-9586afc7f560)

## Helpdesk Easy Questions

1. There are three issues that include the words "index" and "Oracle". Find the call_date for each of them

```sql
SELECT call_date, call_ref FROM Issue
WHERE detail LIKE '%index%' AND detail LIKE '%Oracle%';
```
---
2. Samantha Hall made three calls on 2017-08-14. Show the date and time for each.

```sql
SELECT call_date, first_name, last_name FROM Issue
JOIN Staff ON staff_code=taken_by
WHERE first_name='Samantha' AND last_name='Hall'
AND DATE(call_date)='2017-08-14';
```
---
3. There are 500 calls in the system (roughly). Write a query that shows the number that have each status.

```sql
SELECT status, COUNT(*) AS Volume FROM Issue
GROUP BY status;
```
---
4. Calls are not normally assigned to a manager but it does happen. How many calls have been assigned to staff who are at Manager Level?

```sql
SELECT COUNT(*) AS mlcc FROM Staff
JOIN Issue ON staff_code=assigned_to
WHERE level_code IN (SELECT level_code FROM Level WHERE manager='Y')
GROUP BY level_code;
```
---
5. Show the manager for each shift. Your output should include the shift date and type; also the first and last name of the manager.

```sql
SELECT Shift.shift_date, Shift.shift_type, Staff.first_name, Staff.last_name FROM Staff
JOIN Shift ON Staff.staff_code=Shift.manager
ORDER BY Shift.shift_date;
```
&nbsp;

## Helpdesk Medium Questions

6. List the Company name and the number of calls for those companies with more than 18 calls.

```sql
SELECT company_name, COUNT(*) cc FROM Caller
JOIN Customer ON Customer.company_ref=Caller.company_ref
JOIN Issue ON Caller.caller_id=Issue.caller_id
GROUP BY Customer.company_name
HAVING cc>18;
```
---
7. Find the callers who have never made a call. Show first name and last name

```sql
SELECT first_name, last_name FROM Caller
WHERE caller_id NOT IN (SELECT caller_id FROM Issue);
```
---
8. For each customer show: Company name, contact name, number of calls where the number of calls is fewer than 5

```sql
SELECT Customer.company_name, Caller.first_name, Caller.last_name, COUNT(*) nc FROM Customer
JOIN Caller ON Customer.company_ref=Caller.company_ref
JOIN Issue ON Caller.caller_id=Issue.caller_id
GROUP BY Customer.company_name
HAVING nc<5;
```
---
