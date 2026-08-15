# Templetry Renovate preset

One dependency policy for every Templetry repository, in one place.

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>Templetry/renovate-config"]
}
```

Renovate resolves `github>Templetry/renovate-config` to [`default.json`](default.json) here.

## Why template repos need this more than ordinary ones

A template's dependencies are what **every generated project starts from**. When they rot, the damage does not show up in this repository — it shows up months later in someone else's project, at the worst possible moment. Keeping them current is not maintenance hygiene; it is the product.

The loop this closes:

1. Renovate opens a PR bumping a dependency inside a form.
2. The parent's **Verify** workflow renders that form and builds the output with the real toolchain.
3. Green means the upgrade is safe for every project generated from it. Red means we found the break before any user did.

## Policy

| | |
|---|---|
| Schedule | Weekly, before 6am on Monday (Europe/Madrid) |
| minor / patch | Grouped into a single PR |
| major | One PR each, labelled — always read by a human |
| security advisories | Immediately, ignoring the schedule |
| lock files | Refreshed monthly |
| automerge | **Never.** A template change is a product decision |

## Enabling it

Install the [Renovate GitHub App](https://github.com/apps/renovate) on the `Templetry` organization. Every repository carrying a `renovate.json` picks the policy up from here; this repo also acts as the org-wide onboarding default.

## Related

Generated projects get the same idea as an adoptable piece: `templetry add renovate` ([Templetry/pieces](https://github.com/Templetry/pieces)).
