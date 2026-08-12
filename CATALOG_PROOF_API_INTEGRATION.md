# Automate catalog QA with Phoenix Catalog Proof

Use this integration when a deployment, migration or feed sync must leave a repeatable evidence trail.

Phoenix Catalog Proof compares an approved catalog with a current catalog, stores every finding in the Apify dataset and creates `REPORT.html`, `REPORT.csv` and `REPORT.json`.

## 1. Prepare the input

Save this as `input.json` and replace the example URLs with public catalog feeds you own or are authorized to process.

```json
{
  "baseline": {
    "sourceType": "url",
    "label": "Approved export",
    "url": "https://example.com/catalog-approved.csv",
    "format": "auto"
  },
  "current": {
    "sourceType": "url",
    "label": "Live export",
    "url": "https://example.com/catalog-live.csv",
    "format": "auto"
  },
  "matchingKeys": ["sku", "gtin", "id", "productUrl"],
  "settings": {
    "checkImageUrls": true,
    "checkProductUrls": true,
    "inspectCanonicals": false,
    "maxUrlChecks": 500,
    "priceTolerance": 0.01
  }
}
```

## 2. Start a run through the Apify API

Set your Apify token in an environment variable. Do not commit the token.

```bash
export APIFY_TOKEN="replace-with-your-token"

curl --fail-with-body \
  --request POST \
  --header "Authorization: Bearer $APIFY_TOKEN" \
  --header "Content-Type: application/json" \
  --data @input.json \
  "https://api.apify.com/v2/acts/phoenix-tools~phoenix-catalog-proof/runs?waitForFinish=120&maxTotalChargeUsd=0.10"
```

The `maxTotalChargeUsd` parameter provides a hard run-cost ceiling. Phoenix Catalog Proof is priced at $0.05 per started block of 1,000 products in the larger catalog; check the current Apify Pricing tab before running.

## 3. Use the result

The run response contains the default dataset and key-value store identifiers. Use them in your existing Apify, Make, Zapier, webhook or CI workflow.

A release gate can:

1. fail or pause when critical or high findings exist;
2. attach `REPORT.html` to a client handover;
3. archive `REPORT.csv` for spreadsheet review;
4. retain `REPORT.json` for an automated audit trail;
5. require a human GO, HOLD or ROLL BACK decision.

## Safety

- Use only catalog data and URLs you own or are authorized to process.
- Do not include customer records, secrets, credentials or API tokens in feeds.
- The Actor is read-only and does not log in to or modify ecommerce stores.
- Start with URL checks disabled for a fast data-only test, then enable them for release evidence.

[Run Phoenix Catalog Proof on Apify](https://apify.com/phoenix-tools/phoenix-catalog-proof)

[Try the copy-paste catalog demo](CATALOG_PROOF_DEMO.md)
