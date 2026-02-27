# sustainable-npm<!-- omit in toc -->

![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/lowlydba/sustainable-npm/benchmark.yml?logoColor=blue&label=benchmark&color=blue)
[![Test action](https://github.com/lowlydba/sustainable-npm/actions/workflows/test.yml/badge.svg)](https://github.com/lowlydba/sustainable-npm/actions/workflows/test.yml)
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
      - uses: lowlydba/sustainable-npm@v2
```

To override any defaults:

```yaml
- uses: lowlydba/sustainable-npm@v2
  with:
    audit: 'true'
    fund: 'false'
    progress: 'false'
    save: 'false'
    update-notifier: 'false'
    loglevel: 'warn'
```

The npm configuration is only printed when [debug logging][debug-logging] is enabled (`RUNNER_DEBUG == 'true'`).

## Inputs

| Input             | Description                                                                          | Allowed Values                                                | Default   |
|-------------------|--------------------------------------------------------------------------------------|---------------------------------------------------------------|-----------|
| `audit`           | Run a security audit after install.                                                  | `'true'` or `'false'`                                         | `'false'` |
| `fund`            | Show funding messages.                                                               | `'true'` or `'false'`                                         | `'false'` |
| `progress`        | Show a progress bar during npm operations.                                           | `'true'` or `'false'`                                         | `'false'` |
| `save`            | Automatically update `package.json` when installing packages.                        | `'true'` or `'false'`                                         | `'false'` |
| `update-notifier` | Check for npm updates after each command.                                            | `'true'` or `'false'`                                         | `'false'` |
| `prefer-offline`  | Use cached data without checking for staleness. Uncached packages are still fetched. | `'true'` or `'false'`                                         | `'true'`  |
| `loglevel`        | npm log level.                                                                       | `silent`, `error`, `warn`, `http`, `info`, `verbose`, `silly` | `'error'` |

## Breaking Changes

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

Add a badge to your repo:

[![sustainable-npm](https://img.shields.io/badge/sustainable--npm-🌱-blue?style=flat)](https://github.com/lowlysre/sustainable-npm)

```md
[![sustainable-npm](https://img.shields.io/badge/sustainable--npm-🌱-blue?style=flat)](https://github.com/lowlysre/sustainable-npm)
```

[debug-logging]: https://docs.github.com/en/actions/managing-workflow-runs-and-deployments/managing-workflow-runs/re-running-workflows-and-jobs#about-re-running-workflows-and-jobs
