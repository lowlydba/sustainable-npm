# sustainable-npm<!-- omit in toc -->

![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/lowlydba/sustainable-npm/benchmark.yml?logoColor=blue&label=benchmark&color=blue)
[![Test action](https://github.com/lowlydba/sustainable-npm/actions/workflows/test.yml/badge.svg)](https://github.com/lowlydba/sustainable-npm/actions/workflows/test.yml)
![sustainable-npm](https://img.shields.io/badge/sustainable--npm-🌱-blue?style=flat)

sustainable-npm is a lightweight GitHub Action that globally sets eco-friendly npm configurations to optimize your workflows. By disabling certain npm features (like audit and update notifications), this action helps speed up installations and reduce the carbon footprint of your CI processes.

* 🔒 dependency-free
* ⚛️ small size
* 💰 saves time & money
* 🌎 reduces carbon emissions
* :octocat: pairs seamlessly with [`actions/setup-node`](https://github.com/actions/setup-node) and all active Node LTS versions

---

- [Philosophy](#philosophy)
- [Usage](#usage)
  - [Basic Usage](#basic-usage)
  - [Customizing Inputs](#customizing-inputs)
  - [Debug Logging](#debug-logging)
- [Inputs](#inputs)
- [Environmental Impact](#environmental-impact)
- [Performance Benchmarks](#performance-benchmarks)
- [Contributing](#contributing)
- [Show Your Support](#show-your-support)

## Philosophy

Every millisecond of compute time counts—not only for performance but also for sustainability. sustainable-npm is designed with the environment in mind. By streamlining npm’s behavior, we aim to reduce unnecessary energy usage and carbon emissions, all while making your development pipeline leaner and faster.

## Usage

### Basic Usage

After setting up Node with `actions/setup-node`, simply add this step to configure your npm settings with the eco-friendly defaults:

```yaml
jobs:
  test:
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v3
      - uses: lowlydba/sustainable-npm@v1
```

### Customizing Inputs

If you need to override the defaults:

```yaml
- uses: lowlydba/sustainable-npm@v1
  with:
    audit: 'true'
    fund: 'false'
    progress: 'false'
    save: 'false'
    update-notifier: 'false'
    loglevel: 'warn'
```

### Debug Logging

This workflow skips the `lowlydba/sustainable-npm` action when [debug logging][debug-logging] is enabled (`ACTIONS_STEP_DEBUG == 'true'`), ensuring full output for troubleshooting.

```yaml
jobs:
  test:
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v3
      - uses: lowlydba/sustainable-npm@v1
        if: ${{ env.ACTIONS_STEP_DEBUG != 'true' }}
```

## Inputs

| Input             | Description                                                                                                                                                 | Allowed Values                                        | Default   |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------|-----------|
| `audit`           | Controls whether npm performs a security audit after installing packages. Disabling the audit can improve installation speed.                              | `'true'` or `'false'`                                 | `'false'` |
| `fund`            | Enables or disables npm funding messages. Disabling it reduces unnecessary prompts in CI environments.                                                     | `'true'` or `'false'`                                 | `'false'` |
| `progress`        | Determines if a progress bar is displayed during npm operations. Disabling it minimizes logging overhead.                                                    | `'true'` or `'false'`                                 | `'false'` |
| `save`            | Controls whether npm automatically updates `package.json` with installed dependencies. Disabling this can prevent unintended file changes.                | `'true'` or `'false'`                                 | `'false'` |
| `update-notifier` | Configures whether npm checks for updates to itself after executing commands. Disabling this reduces unnecessary network requests and delays.             | `'true'` or `'false'`                                 | `'false'` |
| `prefer-offline` | Configures whether npm checks for staleness in cached data. Missing data will still be fetched online. Disabling this can reduce unnecessary network requests. | `'true'` or `'false'`                                 | `'true'` |
| `loglevel`        | Sets the logging level for npm. Options include: `silent`, `error`, `warn`, `http`, `info`, `verbose`, and `silly`.                                           | `silent`, `error`, `warn`, `http`, `info`, `verbose`, `silly` | `'error'` |

## Environmental Impact

By using sustainable-npm, you're optimizing one of the most repeated actions in development: `npm install`. With frequent usage, small improvements in time and energy efficiency can lead to significant environmental benefits. Reducing unnecessary operations means lower energy consumption and a smaller carbon footprint.

Every optimization contributes to a more sustainable development process.

## Performance Benchmarks

Below are some example performance benchmarks using [hyperfine](https://github.com/sharkdp/hyperfine). These benchmarks compare npm commands with and without eco-friendly configurations:

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

On average, benchmarking shows a **10-20% reduction in npm install duration** for projects with around 500 package dependencies.

Packages were downloaded in advance before both benchmarks to avoid networking variations on timings.

> [!NOTE]
> The above numbers are *illustrative*. Your actual performance gains will depend on your configuration, network conditions, operating system, and project.

## Contributing

Contributions are welcome! Please open an issue or submit a pull request if you have suggestions, improvements, or encounter any issues.

## Show Your Support

If you're using sustainable-npm, you can add this badge to your repository to spread the word!

![sustainable-npm](https://img.shields.io/badge/sustainable--npm-🌱-blue?style=flat)

```md
![sustainable-npm](https://img.shields.io/badge/sustainable--npm-🌱-blue?style=flat)
```

Want to link back to this project?

```md
[![sustainable-npm](https://img.shields.io/badge/sustainable--npm-🌱-blue?style=flat)](https://github.com/lowlysre/sustainable-npm)
```

This helps promote sustainability in open source by encouraging more developers to reduce unnecessary npm operations. 🌍♻️

[debug-logging]: https://docs.github.com/en/actions/managing-workflow-runs-and-deployments/managing-workflow-runs/re-running-workflows-and-jobs#about-re-running-workflows-and-jobs
