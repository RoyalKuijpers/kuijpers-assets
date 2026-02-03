# Security Policy

## Reporting Security Issues

If you discover a security vulnerability in this repository, please report it to the repository maintainers immediately.

## Secret Scanning

This repository uses automated secret scanning to prevent the accidental commit of sensitive information such as:
- API keys
- Access tokens
- Passwords
- Private keys
- Other credentials

### Automated Checks

A GitHub Actions workflow (`.github/workflows/secret-scanning.yml`) runs on:
- Every push to `main` or `master` branches
- Every pull request
- Manual trigger via workflow dispatch

This workflow uses [Gitleaks](https://github.com/gitleaks/gitleaks) to scan for secrets in the codebase.

## Known Security Issues (Resolved)

### ⚠️ IMPORTANT: Exposed API Key - Action Required

**Date**: February 3, 2026  
**Status**: File deleted from repository

An API key was found hardcoded in the following file (now removed):
- File: `workflows/BadgeregistratieUpdateEHSTrainingsdataopBadgeregis-6ABF458A-A04A-F011-877A-7C1E525DA2D9.json`
- Key: `Apikey 478800b36bd544e29fd86ff69a9ba65a`
- Service: Intelex API (https://eu.intelex.com)

**Action Required**: 
- The exposed API key **MUST be rotated/revoked** on the Intelex platform immediately
- Contact your Intelex administrator to generate a new API key
- The old key remains in git history, so it should be considered compromised

### Best Practices

To prevent future security issues:

1. **Never commit secrets**: Use environment variables or GitHub Secrets instead
2. **Use .gitignore**: Add patterns to exclude files that might contain secrets
3. **Review before commit**: Always review your changes before committing
4. **Rotate exposed keys**: If a secret is accidentally committed, rotate it immediately
5. **Use the workflow**: The secret scanning workflow will catch most common patterns

## Secure Configuration

When working with APIs or external services:
- Use GitHub Secrets to store sensitive values
- Reference secrets in workflows using `${{ secrets.SECRET_NAME }}`
- Never hardcode credentials in JSON, YAML, or code files
