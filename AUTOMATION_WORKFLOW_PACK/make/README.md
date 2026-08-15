# Make HTTP recipes

These JSON files are transparent configuration recipes for **HTTP > Make a request**. They are not Make blueprints and do not pretend to offer one-click import.

For each recipe:

1. Add a manual input source or custom webhook.
2. Add **HTTP > Make a request**.
3. Copy `method`, `url`, `headers` and `body` from the recipe.
4. Replace the example value or map it from the previous module.
5. Run once manually and review the JSON response before adding any schedule or downstream action.

No Phoenix API needs credentials. Tool-specific limits remain visible on the public Phoenix Tools page.
