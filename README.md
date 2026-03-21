# sustainable-npm<!-- omit in toc -->

[![Test action](https://github.com/lowlydba/sustainable-npm/actions/workflows/test.yml/badge.svg)](https://github.com/lowlydba/sustainable-npm/actions/workflows/test.yml)
![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/lowlydba/sustainable-npm/benchmark.yml?logo=github&label=benchmark&color=green)
[![immutable release ruleset](https://img.shields.io/badge/immutable%20tags-active-green?logo=github)](https://github.com/lowlydba/sustainable-npm/rules/14185577)
![sustainable-npm](https://img.shields.io/badge/sustainable--npm-🌱-blue?style=flat)

<img width="800" height="422" alt="sustainable-npm-og" src="https://github.com/user-attachments/assets/e963c345-e370-47ce-b970-1b812e369c64" />

A lightweight GitHub Action that sets sensible npm defaults to speed up installs and cut unnecessary energy use in CI.

* 🔒 dependency-free
* ⚛️ small size
* 💰 saves time & money
* 🌎 reduces carbon emissions
* :octocat: pairs seamlessly with [`actions/setup-node`](https://github.com/actions/setup-node) and all active Node LTS versions

---

- [Usage](#usage)
- [Inputs](#inputs)
- [Breaking Changes](#breaking-changes)
  - [v3.0.0](#v300)
  - [v2.0.0](#v200)
- [Performance Benchmarks](#performance-benchmarks)
- [Real-World Performance](#real-world-performance)
- [Show Your Support](#show-your-support)

## Usage

After setting up Node with `actions/setup-node`, add this step:

```yaml
jobs:
  test:
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v3
      - uses: lowlydba/sustainable-npm@v3
```

To override any defaults:

```yaml
- uses: lowlydba/sustainable-npm@v3
  with:
    audit: 'true'
    fund: 'false'
    progress: 'false'
    update-notifier: 'false'
    loglevel: 'warn'
    ignore-scripts: 'false'
```

The npm configuration is only printed when [debug logging][debug-logging] is enabled (`RUNNER_DEBUG == 'true'`).

> [!TIP]
> SemVer tags (e.g. `v3.0.0`) and superseded major tags (e.g. `v2`) are immutable, enforced via [repository rulesets](https://github.com/lowlydba/sustainable-npm/rules). For maximum supply chain security, [pin to a full commit SHA](https://docs.github.com/en/actions/security-for-github-actions/security-guides/security-hardening-for-github-actions#using-third-party-actions) rather than a tag.

## Inputs

| Input             | Description                                                                                                                        | Allowed Values                                                 | Default   |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------|-----------|
| `audit`           | Run a security audit after install.                                                                                                | `'true'` or `'false'`                                          | `'false'` |
| `fund`            | Show funding messages.                                                                                                             | `'true'` or `'false'`                                          | `'false'` |
| `progress`        | Show a progress bar during npm operations.                                                                                         | `'true'` or `'false'`                                          | `'false'` |
| `update-notifier` | Check for npm updates after each command.                                                                                          | `'true'` or `'false'`                                          | `'false'` |
| `prefer-offline`  | Use cached data without checking for staleness. Uncached packages are still fetched.                                               | `'true'` or `'false'`                                          | `'true'`  |
| `loglevel`        | npm log level.                                                                                                                     | `silent`, `error`, `warn`, `http`, `info`, `verbose`, `silly`  | `'error'` |
| `ignore-scripts`  | Prevent npm from running lifecycle scripts (e.g. `postinstall`). Reduces install time and protects against supply chain attacks.   | `'true'` or `'false'`                                          | `'true'`  |

## Breaking Changes

### v3.0.0

`ignore-scripts` is now enabled by default (`true`). This prevents npm from running lifecycle scripts (e.g. `postinstall`) during installs, protecting against supply chain attacks via malicious packages. If your project relies on install scripts from trusted dependencies, set `ignore-scripts: 'false'` to restore the previous behavior.

### v2.0.0

The "Print npm configs" step now only runs when debug logging is enabled (`RUNNER_DEBUG == 'true'`). To re-enable it, set that variable in your workflow.

## Performance Benchmarks

Benchmarks via [hyperfine](https://github.com/sharkdp/hyperfine), 20 runs with 3 warmups:

```bash
$ hyperfine 'npm install' 'npm install --audit=false --fund=false --loglevel=error --update-notifier=false --progress=false' --ignore-failure --runs 20 --warmup 3

Benchmark 1: npm install
  Time (mean ± σ):      2.172 s ±  0.097 s    [User: 1.958 s, System: 0.750 s]
  Range (min … max):    2.017 s …  2.347 s    20 runs

Benchmark 2: npm install --audit=false --fund=false --loglevel=error --update-notifier=false --progress=false
  Time (mean ± σ):      1.849 s ±  0.107 s    [User: 1.819 s, System: 0.668 s]
  Range (min … max):    1.626 s …  2.046 s    20 runs

Summary
  npm install --audit=false --fund=false --loglevel=error --update-notifier=false --progress=false ran
    1.17 ± 0.09 times faster than npm install
```

Around a **10-20% reduction in install time** on projects with ~500 dependencies. Packages were pre-downloaded to keep network conditions out of the equation.

> [!NOTE]
> Your actual gains will vary based on project size, network, and OS.

## Real-World Performance

* [rvandernoort details results using EcoCI in #11](https://github.com/lowlydba/sustainable-npm/issues/11#issuecomment-3908732169)

## Show Your Support

Add a badge to your repository:

[![sustainable-npm](https://img.shields.io/badge/sustainable--npm-🌱-blue?style=flat)](https://github.com/lowlysre/sustainable-npm)

```md
[![sustainable-npm](https://img.shields.io/badge/sustainable--npm-🌱-blue?style=flat)](https://github.com/lowlysre/sustainable-npm)
```

[debug-logging]: https://docs.github.com/en/actions/managing-workflow-runs-and-deployments/managing-workflow-runs/re-running-workflows-and-jobs#about-re-running-workflows-and-jobs
