# Gruyere XSS Report

## Bug Report: Stored Cross-Site Scripting (XSS)

**Severity:** High

**Summary:**
The snippet creation functionality in Google Gruyere does not sanitize user input, allowing injection of malicious JavaScript that executes in the browser of any user viewing the snippet.

**Steps to Reproduce:**
1. Sign up for Gruyere account at `https://google-gruyere.appspot.com`
2. Click "New Snippet"
3. Enter title: `XSS Test`
4. Enter content: `<script>alert('XSS')</script>`
5. Submit snippet
6. Visit snippet page — JavaScript alert executes

**Impact:**
- Session hijacking (steal user cookies)
- Phishing attacks (redirect to fake login)
- Website defacement
- Keylogging of user keystrokes

**Proof of Concept:**

Payload used: `<script>alert('XSS')</script>`

Result: Upon viewing the snippet, browser executed JavaScript and displayed alert box with text "XSS", confirming stored XSS vulnerability.

**Remediation:**
Sanitize all user input before display:
```php
$content = htmlspecialchars($user_input, ENT_QUOTES, 'UTF-8');
