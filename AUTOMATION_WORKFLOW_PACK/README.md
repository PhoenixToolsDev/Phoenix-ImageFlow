# Phoenix Automation Workflow Pack 1.0

Four ready-to-import n8n workflows and matching Make HTTP recipes for the public Phoenix Audit Suite APIs.

- [Open the workflow pack page](https://phoenix-tools.michel-goossens99.chatgpt.site/automation-workflow-pack)
- [Download the complete ZIP](https://phoenix-tools.michel-goossens99.chatgpt.site/downloads/Phoenix_Automation_Workflow_Pack_v1.0.zip)
- [Try the accessibility pre-audit](https://phoenix-tools.michel-goossens99.chatgpt.site/accessibility-pre-audit)
- [Try the security baseline](https://phoenix-tools.michel-goossens99.chatgpt.site/website-security-baseline)
- [Try the product price monitor](https://phoenix-tools.michel-goossens99.chatgpt.site/product-price-monitor)
- [Try the tender/RFP analyzer](https://phoenix-tools.michel-goossens99.chatgpt.site/tender-rfp-analyzer)

## Included workflows

1. Website accessibility pre-audit
2. Website security-header baseline
3. Product price and availability snapshot
4. Tender/RFP requirements extraction

## n8n

Import one JSON file from the `n8n` folder. Open the `Set input` node, replace the fictional input, then execute the workflow manually. No credentials are required.

The workflows use only built-in Manual Trigger, Edit Fields and HTTP Request nodes. They make one bounded POST request to a public Phoenix Tools API. They do not schedule themselves, contact anyone, submit a bid, buy anything or write to an external account.

## Make

The `make` folder contains one JSON request recipe per API. In a new scenario, add **Webhooks > Custom webhook** or a manual input source, then **HTTP > Make a request**. Copy the method, URL, headers and JSON body from the matching recipe. The files are configuration recipes, not Make blueprints, so they do not claim one-click import compatibility.

## Safety and privacy

- Public URLs or user-supplied tender text only.
- No local/private destinations, crawling, authentication bypass or exploitation.
- No server-side history in the price or tender tools.
- Results are first-pass evidence, not certification, legal advice, eligibility decisions or authoritative monitoring.
- Always review the original source and the tool-specific limits.

## Test inputs

- Public-page workflows default to `https://example.com`.
- The tender workflow includes a fictional request for proposal.
- Run manually before adding any schedule or downstream action.

Released by Phoenix Tools on 15 August 2026.
