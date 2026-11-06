# Security policy

## Supported versions

The latest code on the default branch is the maintained version of this portfolio project. There is no formal release support schedule.

## Reporting vulnerabilities

Please avoid posting credentials, private API responses, access tokens, or other sensitive data in public issues.

If you identify a security flaw, use GitHub's **Report a vulnerability** / private vulnerability reporting option if it is enabled for this repository. Otherwise, open a public issue containing **only a sanitized description** and ask the maintainer for a private reporting channel.

Include a reproducible test case with synthetic data, expected behavior, observed behavior, and impact. Do not publish exploit details that expose a real third party.

## Security boundaries

- APIGuard inspects user-supplied response data locally in the browser; it is not an active scanner.
- JWT inspection is not signature verification.
- Findings are heuristic and should be independently validated.
- Secret masking is best-effort. Review reports before sharing and never submit live production secrets.
- Only analyze systems and data you own or have permission to assess.
