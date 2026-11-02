# SQL Injection Assessment

## 1. Lab Environment

- Application: DVWA
- Target: Metasploitable 2
- Target IP: 192.168.50.20
- Testing machine: Kali Linux
- Testing tool: Firefox

## 2. Vulnerability Identified

SQL Injection (SQLi).

## 3. Testing

At Low security level, the following test input was submitted:

`1' OR '1'='1`

## 4. Observed Result

The application returned five database records instead of restricting the result to User ID 1.

## 5. Technical Explanation

The application incorporated untrusted input directly into an SQL query.

The condition `'1'='1'` evaluates to TRUE, changing the query logic and allowing multiple records to be returned.

## 6. Security Impact

Potential consequences include:

- Unauthorized database access.
- Exposure of confidential records.
- Authentication bypass in vulnerable applications.
- Unauthorized database modification, depending on database permissions.

## 7. Recommended Mitigations

- Use prepared statements and parameterized queries.
- Validate input on the server side.
- Apply least-privilege database permissions.
- Avoid exposing detailed database errors.
- Conduct regular security testing.

## 8. Conclusion

The assessment successfully demonstrated SQL Injection in DVWA at Low security level.

The application returned all five user records because the submitted input altered the SQL query's logical condition.
