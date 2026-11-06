# APIGuard

**Browser-based API response security analyzer** — inspect HTTP responses, identify potential security misconfigurations, and export evidence-based reports.

[Open the app source](./index.html) · [Security policy](./SECURITY.md)

## What it does

APIGuard analyzes **response data supplied by the user**. It is designed for developers, students, and security practitioners reviewing APIs they own or are authorized to assess.

- Reviews response status, headers, body, authentication context, and endpoint URL.
- Flags potentially exposed credentials and sensitive fields.
- Reviews cookie security attributes and selected JWT-related warning signs.
- Highlights potentially sensitive data returned in anonymous-access scenarios.
- Produces findings with severity, evidence, explanations, and report exports.
- Attempts to redact secrets from finding evidence and exported reports.

> **Important:** This is a static, browser-side analyzer. It **does not send HTTP requests**, authenticate to a remote service, validate JWT signatures, or prove exploitability. Findings require human verification. Regex-based redaction is not a guarantee that all secrets are removed.

## Quick start

1. Download or clone the repository.
2. Open `index.html` in a modern browser.
3. Paste a **synthetic or appropriately sanitized** API response and its metadata.
4. Run the analysis and review each finding.
5. Export a report only after checking that it contains no sensitive data.

No backend, API key, or package installation is required for the browser app.

## Example input

Endpoint: `https://api.example.test/v1/account`  
Method: `GET`  
HTTP status: `200`  
Authentication context: *Without authentication*  
Response headers:

```http
Content-Type: application/json
Cache-Control: no-store
```

Response body:

```json
{"account":{"id":42,"email":"demo@example.test"}}
```

This synthetic example can illustrate an exposure warning depending on the selected context and the analyzer's rules; it does **not** establish a real vulnerability without authorization and server-side verification.

## Technology

- HTML5, CSS3, and vanilla JavaScript
- Client-side rule-based analysis
- JSON and HTML report export

## Architecture

```text
User-provided HTTP response
           |
           v
   Input parsing / context
           |
           v
   Security analysis rules
           |
           v
  Findings and redaction
           |
           v
   UI + report exports
```

The application is currently implemented in `index.html`. A separate legacy `(CLI)` file is a Python task-manager prototype and is **not** part of the API analyzer.

## Scope and limitations

- No active network scanning or automatic API requests.
- No JWT cryptographic verification.
- Potential issues are heuristics, not confirmed vulnerabilities.
- Redaction is best-effort; do not paste production secrets.
- Run against data you own or are permitted to assess.

## Development roadmap

- [ ] Extract analysis logic into independently testable JavaScript modules.
- [ ] Add automated tests for redaction and false-positive cases.
- [ ] Add CI checks with GitHub Actions.
- [ ] Improve JWT claims inspection without implying signature validation.
- [ ] Add screenshots and a hosted demo.

## Responsible use

See [SECURITY.md](./SECURITY.md) for reporting guidance and safe-handling expectations.

---
Built as a software engineering and API security portfolio project.
