# Copilot Instructions for sustainable-npm

## Pull Request Descriptions


### Body

**What changed** — one or two sentences describing the change to `action.yml`, inputs, or supporting files.

**Why** — the motivation: performance gain, security improvement, reduced CI noise, etc. Tie it back to the action's goals where applicable (faster installs, lower energy use, supply chain safety).

**Breaking change** (if applicable) — call out any default value changes or removed inputs explicitly. State what users need to do to preserve previous behavior.

**Testing** — mention that the `test.yml` workflow covers the change, and note any matrix dimensions relevant to the fix (OS, Node version).

### What to omit
- Do not include a checklist or checkbox items.
- Do not include "no breaking changes" boilerplate when there are none — just omit the section.
- Do not pad with filler phrases like "This PR aims to..." or "I have tested this by...".
- Do not reference issue numbers unless they are known.

## Versioning & Pinning

- Semver tags (e.g. `v3.0.0`) are immutable once pushed and are never force-pushed.
- The current major floating tag (e.g. `v3`) tracks the latest release on that major line and is mutable.
- Previous major floating tags (e.g. `v2`) are converted to immutable once superseded by a new major.
- These rules are enforced via [repository rulesets](https://github.com/lowlydba/sustainable-npm/rules).
- For best security, users should [pin to a full commit SHA](https://docs.github.com/en/actions/security-for-github-actions/security-guides/security-hardening-for-github-actions#using-third-party-actions) rather than a tag.
- When suggesting usage examples in PR descriptions or docs, prefer the current major tag; if the context is security-hardening, suggest SHA pinning.

## General Coding Conventions

- This is a composite GitHub Action — `action.yml` is the only source code. There is no build step.
- All inputs are optional strings; booleans are passed as `'true'` / `'false'`.
- Input values must be passed through `env:` variables before use in shell scripts to prevent injection.
- Shell is always `bash`. Use 2-space indentation in YAML.
- Debug output must be gated on `runner.debug` / `if: runner.debug`.
