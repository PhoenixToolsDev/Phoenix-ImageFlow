# Phoenix Catalog Proof — 5-minute ecommerce migration check

Phoenix Catalog Proof compares an approved catalog with a current or live catalog before a Shopify, WooCommerce, marketplace, PIM, ERP, feed, or client handover release.

Run the Actor on Apify:

https://apify.com/phoenix-tools/phoenix-catalog-proof

## Minimal test data

Save this as `baseline.json`:

```json
[
  {
    "sku": "PHX-MUG-001",
    "title": "Black mug",
    "price": 19.99,
    "currency": "EUR",
    "stock": 12,
    "image": "https://example.com/images/black-mug.jpg",
    "productUrl": "https://example.com/products/black-mug"
  },
  {
    "sku": "PHX-TEE-001",
    "title": "Phoenix T-shirt",
    "price": 24.99,
    "currency": "EUR",
    "stock": 8,
    "image": "https://example.com/images/phoenix-tee.jpg",
    "productUrl": "https://example.com/products/phoenix-tee"
  }
]
```

Save this as `current.json`:

```json
[
  {
    "sku": "PHX-MUG-001",
    "title": "Black mug",
    "price": 21.99,
    "currency": "EUR",
    "stock": 0,
    "image": "https://example.com/images/black-mug.jpg",
    "productUrl": "https://example.com/products/black-mug"
  },
  {
    "sku": "PHX-CAP-001",
    "title": "Phoenix cap",
    "price": 17.99,
    "currency": "EUR",
    "stock": 15,
    "image": "https://example.com/images/phoenix-cap.jpg",
    "productUrl": "https://example.com/products/phoenix-cap"
  }
]
```

Use the baseline as the approved source and current as the new source. The comparison should surface:

- the T-shirt removed from the current catalog;
- the cap added to the current catalog;
- the mug price changed from EUR 19.99 to EUR 21.99;
- the mug stock changed from 12 to 0.

Enable image and product URL checks only when the URLs are real public URLs that you own or are authorized to audit. The Actor is read-only and does not require a store login. It creates HTML, CSV, and JSON evidence reports, while the complete finding list remains in the Apify dataset.

Use only authorized catalog data. Never include customer records, secrets, API tokens, or personal data in a feed.
