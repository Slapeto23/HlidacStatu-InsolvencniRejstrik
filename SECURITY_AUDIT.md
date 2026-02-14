# Security Audit Report - Sensitive Data Scan

**Date:** 2026-02-14
**Scope:** All public repositories of Slapeto23

## Repositories Audited

| # | Repository | Status |
|---|-----------|--------|
| 1 | Slapeto23/HlidacStatu-InsolvencniRejstrik | Clean |
| 2 | Slapeto23/tanstack-template | Clean |
| 3 | Slapeto23/Slapeto23 | 2 findings (see below) |
| 4 | Slapeto23/packaging.python.org | Clean |
| 5 | Slapeto23/servers | Clean |
| 6 | Slapeto23/pi-explorer | Clean |
| 7 | Slapeto23/nextjs-ai-chatbot | Does not exist |
| 8 | Slapeto23/desktop-tutorial | Does not exist |

## Findings

### Finding 1: Hardcoded Default JWT Secret (Medium Severity)

- **Repository:** `Slapeto23/Slapeto23`
- **File:** `src/auth.js`, line 6
- **Content:** `const DEFAULT_SECRET = 'default-secret-change-in-production';`
- **Risk:** If `AuthModule` is instantiated without a custom `secret` option, JWTs are signed with this publicly known string, enabling token forgery.
- **Recommendation:** Remove the default value and throw an error when `secret` is not provided.

### Finding 2: Internal Proxy URL in package.json (Low Severity)

- **Repository:** `Slapeto23/Slapeto23`
- **File:** `package.json`, repository URL field
- **Content:** `"url": "http://local_proxy@127.0.0.1:58388/git/Slapeto23/Slapeto23"`
- **Risk:** Exposes internal development infrastructure details (local Git proxy on port 58388). No password is embedded.
- **Recommendation:** Replace with standard GitHub URL: `https://github.com/Slapeto23/Slapeto23.git`

## Summary

**No real secrets (API keys, passwords, tokens, private keys, or database credentials) were found in any repository.** All repositories follow good practices:

- `.env` files are properly gitignored where applicable
- Sensitive values are read from environment variables at runtime
- README examples and `.env.example` files contain only obvious placeholders
- CI/CD workflows use GitHub Secrets / OIDC, not hardcoded values

The two findings in `Slapeto23/Slapeto23` are security anti-patterns rather than actual credential leaks, but should still be addressed.
