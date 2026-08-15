# Phoenix Audit Suite API v1.0

Four public, bounded utilities for developers and automation builders. No Phoenix API key, account, subscription, or scheduler is required.

## Import

- [OpenAPI 3.1 specification](PHOENIX_AUDIT_SUITE_OPENAPI.json)
- [Postman Collection v2.1](PHOENIX_AUDIT_SUITE.postman_collection.json)
- [Raw OpenAPI URL](https://raw.githubusercontent.com/PhoenixToolsDev/Phoenix-ImageFlow/main/PHOENIX_AUDIT_SUITE_OPENAPI.json)
- [Raw Postman URL](https://raw.githubusercontent.com/PhoenixToolsDev/Phoenix-ImageFlow/main/PHOENIX_AUDIT_SUITE.postman_collection.json)

Production base URL:

```text
https://phoenix-tools.michel-goossens99.chatgpt.site
```

## Endpoints

| Tool | POST endpoint | Browser tool |
| --- | --- | --- |
| Accessibility Pre-Audit | `/api/accessibility-pre-audit` | [Open](https://phoenix-tools.michel-goossens99.chatgpt.site/accessibility-pre-audit) |
| Website Security Baseline | `/api/website-security-baseline` | [Open](https://phoenix-tools.michel-goossens99.chatgpt.site/website-security-baseline) |
| Product Price & Availability | `/api/product-price-monitor` | [Open](https://phoenix-tools.michel-goossens99.chatgpt.site/product-price-monitor) |
| Tender & RFP Requirements | `/api/tender-rfp-analyzer` | [Open](https://phoenix-tools.michel-goossens99.chatgpt.site/tender-rfp-analyzer) |

The first three endpoints accept a public URL:

```json
{
  "url": "https://example.com"
}
```

The Tender/RFP Analyzer accepts pasted text:

```json
{
  "text": "RFP ACME-2026-17. Proposals are due 30 September 2026 at 17:00 UTC."
}
```

or a public document URL:

```json
{
  "url": "https://example.com/public-rfp"
}
```

## Quick start

```bash
curl -sS -X POST \
  -H "Content-Type: application/json" \
  -d '{"url":"https://example.com"}' \
  "https://phoenix-tools.michel-goossens99.chatgpt.site/api/accessibility-pre-audit"
```

```javascript
const response = await fetch(
  "https://phoenix-tools.michel-goossens99.chatgpt.site/api/tender-rfp-analyzer",
  {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({
      text: "RFP ACME-2026-17. Proposals are due 30 September 2026 at 17:00 UTC."
    })
  }
);

if (!response.ok) {
  throw new Error(`Phoenix API returned ${response.status}`);
}

console.log(await response.json());
```

## Automation pack

Prefer a visual workflow?

- [Open the four importable n8n workflows](AUTOMATION_WORKFLOW_PACK/README.md)
- [Download the complete workflow ZIP](https://phoenix-tools.michel-goossens99.chatgpt.site/downloads/Phoenix_Automation_Workflow_Pack_v1.0.zip)
- [Run the Tender/RFP Analyzer demo](TENDER_RFP_ANALYZER_API_DEMO.md)

## Boundaries

- Only submit public URLs or text you are authorized to process.
- The security baseline is passive and is not a penetration test.
- The accessibility result is a pre-audit, not a certification or replacement for manual WCAG testing.
- Product snapshots depend on the structured data and public HTML exposed by the source page.
- Tender/RFP extraction is decision support; verify every deadline and requirement against the source before bidding.
- Calls run only when requested. These resources do not activate a schedule or background monitor.
- Do not submit secrets, credentials, private documents, personal data, or internal-only URLs.
