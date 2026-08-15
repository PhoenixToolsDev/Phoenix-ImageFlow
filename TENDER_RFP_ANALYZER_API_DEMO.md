# Tender/RFP Analyzer API demo

Turn unstructured procurement text into a reviewable evidence map before deciding whether to bid.

- **Try the browser tool:** https://phoenix-tools.michel-goossens99.chatgpt.site/tender-rfp-analyzer
- **API endpoint:** `POST https://phoenix-tools.michel-goossens99.chatgpt.site/api/tender-rfp-analyzer`
- **Ready-made n8n workflow:** [phoenix-tender-rfp-analyzer.json](AUTOMATION_WORKFLOW_PACK/n8n/phoenix-tender-rfp-analyzer.json)
- No account or Phoenix API key is required.

## What it extracts

The response groups source-linked references, deadlines, stated budget or value, mandatory requirements, submission instructions, scope, evaluation criteria and caution passages. It also returns an extraction-completeness summary.

This is a first-review aid. It does not decide eligibility, interpret procurement law, submit a bid or replace verification against the original documents.

## Copy-paste example

The example below is fictional. Replace `text` with tender or RFP text you are allowed to process.

```bash
curl --fail-with-body \
  --request POST \
  --header "Content-Type: application/json" \
  --data '{
    "text": "Public Website Support Services — Request for Proposal\nRFP reference: CITY-2026-WEB-14\nSubmission deadline: 30 September 2026 at 17:00 CET.\nScope: website maintenance and accessibility fixes for 12 months.\nThe supplier must demonstrate three years of relevant experience.\nProposals must be submitted through the procurement portal.\nEstimated contract value: EUR 48,000.\nEvaluation criteria: quality 60%, price 30%."
  }' \
  "https://phoenix-tools.michel-goossens99.chatgpt.site/api/tender-rfp-analyzer"
```

## JavaScript example

```js
const tenderText = `
Public Website Support Services — Request for Proposal
RFP reference: CITY-2026-WEB-14
Submission deadline: 30 September 2026 at 17:00 CET.
Scope: website maintenance and accessibility fixes for 12 months.
The supplier must demonstrate three years of relevant experience.
Proposals must be submitted through the procurement portal.
Estimated contract value: EUR 48,000.
Evaluation criteria: quality 60%, price 30%.
`;

const response = await fetch(
  "https://phoenix-tools.michel-goossens99.chatgpt.site/api/tender-rfp-analyzer",
  {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ text: tenderText }),
  },
);

const result = await response.json();
if (!response.ok) throw new Error(result.error ?? "Analysis failed");

console.log({
  references: result.references,
  deadlines: result.deadlines,
  budgets: result.budgets,
  mandatoryRequirements: result.mandatoryRequirements,
  submissionInstructions: result.submissionInstructions,
  evaluationCriteria: result.evaluationCriteria,
  completeness: result.extractionSummary?.completeness,
});
```

## Expected evidence from the fictional example

Verify the response contains evidence corresponding to:

- reference `CITY-2026-WEB-14`
- deadline `30 September 2026`
- stated value `EUR 48,000`
- the three-year experience requirement
- procurement-portal submission
- the 12-month website-support scope
- quality and price evaluation criteria

The API deliberately returns empty groups when a signal is absent. Do not convert missing evidence into an assumed requirement.

## URL mode

For one public HTML page, send `{"url":"https://example.org/public-tender"}` instead of `text`. Private, local and authenticated destinations are rejected. Redirect count, request time and input size are bounded; the tool does not crawl a portal or bypass anti-bot controls.

## Automation use

Import the [n8n workflow](AUTOMATION_WORKFLOW_PACK/n8n/phoenix-tender-rfp-analyzer.json) for a manual three-node flow, or copy the [Make recipe](AUTOMATION_WORKFLOW_PACK/make/tender-rfp-analyzer-request.json). Both make one bounded request and activate no schedule.

Use the free [complete workflow pack](https://phoenix-tools.michel-goossens99.chatgpt.site/automation-workflow-pack) when you need the matching accessibility, security and product-price checks too.

## Privacy and operating limits

Phoenix does not store submitted text, URLs or analysis results. Aggregate successful-use totals contain no input, output, IP address, cookie, browser detail, referrer or timestamp. Always verify extracted evidence against the source procurement documents before acting.
