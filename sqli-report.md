# SQL Injection Report

## Bug Report: Authentication Bypass via SQL Injection

**Severity:** Critical

**Summary:**
The login functionality in a custom PHP application is vulnerable to SQL injection, allowing attackers to bypass authentication and log in as administrator without valid credentials.

**Steps to Reproduce:**
1. Navigate to login page
2. Enter username: `' OR '1'='1`
3. Enter any password
4. Submit form
5. Observe successful login as administrator

**Impact:**
- Complete authentication bypass
- Unauthorized admin access
- Data theft, modification, or deletion
- Full system compromise

**Proof of Concept:**

Payload used: `' OR '1'='1`

Result: Application logged in as administrator without valid password, confirming SQL injection vulnerability.

**Remediation:**
Use parameterized queries (prepared statements):
```php
$stmt = $pdo->prepare("SELECT * FROM users WHERE username = ? AND password = ?");
$stmt->execute([$username, $password]);
