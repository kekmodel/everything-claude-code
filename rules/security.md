# Security Guidelines

## Mandatory Security Checks

Before ANY commit:
- [ ] No hardcoded secrets (API keys, passwords, tokens)
- [ ] All user inputs validated
- [ ] SQL injection prevention (parameterized queries)
- [ ] XSS prevention (sanitized output)
- [ ] CSRF protection where applicable
- [ ] Authentication/authorization verified
- [ ] Error messages don't leak sensitive data

## Secret Management

```
# NEVER: Hardcoded secrets
api_key = "sk-proj-xxxxx"

# ALWAYS: Environment variables
api_key = os.environ["API_KEY"]
```

Use `.env.example` with placeholders:
```
API_KEY=YOUR_API_KEY_HERE
DATABASE_URL=YOUR_DATABASE_URL_HERE
```

## OWASP Top 10 Awareness

1. Injection - Use parameterized queries
2. Broken Authentication - Strong password policies
3. Sensitive Data Exposure - Encrypt at rest/transit
4. XML External Entities - Disable external entities
5. Broken Access Control - Verify permissions
6. Security Misconfiguration - Review defaults
7. XSS - Escape output
8. Insecure Deserialization - Validate input
9. Known Vulnerabilities - Update dependencies
10. Insufficient Logging - Log security events

## Security Response Protocol

If security issue found:
1. STOP immediately (Principle 3)
2. Assess severity (Critical/High/Medium/Low)
3. Fix CRITICAL issues before continuing
4. Rotate any exposed secrets
5. Review codebase for similar issues

## Dependency Security

- Audit dependencies regularly
- Use lockfiles
- Review before adding new dependencies
- Prefer well-maintained packages

## Supports Principle 2

Security is evidence:
- Security scan results
- Dependency audit output
- No secrets in git history
