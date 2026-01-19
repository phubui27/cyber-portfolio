# WebGoat – HTTP Observation (SOC Perspective)

## Lab context
- Platform: OWASP WebGoat (https://owasp.org/www-project-webgoat/)
- Focus: HTTP request / response behavior
- Perspective: Security Operations Center (SOC)

---

## Observation 1 – Authentication failure pattern

Observed behavior:
- Method: POST
- URL: /login
- Status code: 401
- Multiple attempts from the same source

SOC interpretation:
- Repeated POST requests with 401 indicate possible brute force login attempt

SOC action (real-world scenario):
- Monitor source IP
- Correlate with authentication logs
- Escalate if threshold exceeded

---

## Observation 2 – Access to non-existing admin endpoint

Observed behavior:
- Method: GET
- URL: /admin
- Status code: 404
- Repeated access attempts

SOC interpretation:
- Attempt to discover hidden or restricted admin endpoint

SOC action (real-world scenario):
- Flag IP for monitoring
- Review further web access patterns
