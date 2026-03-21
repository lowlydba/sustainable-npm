# Copilot Instructions for sustainable-npm

## Pull Request Descriptions

When generating a PR description, follow this structure:

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

## General Coding Conventions

- This is a composite GitHub Action — `action.yml` is the only source code. There is no build step.
- All inputs are optional strings; booleans are passed as `'true'` / `'false'`.
- Input values must be passed through `env:` variables before use in shell scripts to prevent injection.
- Shell is always `bash`. Use 2-space indentation in YAML.
- Debug output must be gated on `runner.debug` / `if: runner.debug`.
