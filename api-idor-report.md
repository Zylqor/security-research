# API IDOR Report

## Bug Report: Mass Information Disclosure via /users Endpoint

**Severity:** Critical

**Summary:**
The `/users` endpoint returns complete PII for all users without authentication or pagination. Combined with IDOR in `/users/{id}`, this exposes entire user database.

**Steps to Reproduce:**
```bash
curl "https://jsonplaceholder.typicode.com/users"
