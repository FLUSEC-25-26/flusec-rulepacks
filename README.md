# flusec-rulepacks

Remote rule packs for the FLUSEC VS Code Extension.

This repository allows the FLUSEC team to update detection rules and component configurations without publishing a new extension release. The extension syncs these rule packs, caches them locally, and continues to work offline using the last cached version.

## What is inside

- **Base rules** for each component (pattern rules, metadata, severity, descriptions)
- **Manifest files** to version and control updates
- **Heuristics config** (only for HSD at the moment)

## Folder structure

- `hsd/`
  - `manifest.json`
  - `base_rules.json`
  - `heuristics.json` *(only used by HSD for now)*
- `input_validation/`
  - `manifest.json`
  - `base_rules.json`
- `network/`
  - `manifest.json`
  - `base_rules.json`
- `storage/`
  - `manifest.json`
  - `base_rules.json`

## How FLUSEC uses this repo

1. The extension reads each component’s `manifest.json`
2. If the manifest version changed, it downloads the latest `base_rules.json`
3. For **HSD only**, it also downloads `heuristics.json`
4. Downloads are cached locally to support offline usage
5. Users can force an immediate refresh using the extension’s “Update Rule Packs” command

## Versioning and updates

When you update rules for a component:

1. Edit that component’s `base_rules.json` (and `heuristics.json` for HSD if needed)
2. Increment the `version` in that component’s `manifest.json`
3. Commit and push changes

The version bump is what signals the extension to pull the latest rule pack.

## Guidelines

- Do not store real secrets in this repository.
- Use safe demo values or markers for testing.
- Keep rule IDs stable once published to avoid breaking diagnostics and references in reports.
- Prefer backward-compatible changes; when breaking changes are required, bump the version accordingly and document the change.

## Status

- HSD supports base rules + heuristics.
- input_validation, network, and storage currently support base rules only.
