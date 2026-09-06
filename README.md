# edgecommons component registry

The machine-readable catalog of components in the **edgecommons** ecosystem — protocol adapters,
edge processors, services, bridges, consoles, and northbound sinks built on the
[`edgecommons`](https://github.com/edgecommons/edgecommons) library.

- **`components.json`** — the catalog (source of truth for "what components exist").
- **`registry.schema.json`** — JSON Schema the catalog is validated against in CI.

## Consumers

- **CLI:** `edgecommons registry list|show` reads this catalog. By default the CLI fetches it
  through the GitHub CLI (`gh api .../contents/components.json`).
  Override with `--source <path>` or `$EDGECOMMONS_REGISTRY_URL` set to a local `components.json`
  path. This CLI build rejects HTTP URL sources; the environment variable retains its established
  name. A local source works offline. `registry versions` verifies the component exists, then reports
  the missing release index; it does not discover or enumerate package releases in this build.
- **Docs site:** renders a "Components" page from `components.json`.

## Adding or updating a component

Open a pull request editing `components.json` — see [`CONTRIBUTING.md`](CONTRIBUTING.md). CI validates
the file against the schema before merge.

This repository is public. The CLI's default reader uses the authenticated GitHub CLI; use a local
catalog path when operating offline. The catalog describes discovery and maturity, not a guarantee
that every platform/feature has passed fresh validation. Per-component documentation records those
limits. JSON in this repository is native catalog/schema JSON, not an EdgeCommons message envelope.
