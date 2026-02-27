# Contributing to sustainable-npm

Thank you for your interest in contributing! Contributions of all kinds are welcome — bug reports, feature requests, documentation improvements, and code changes.

## Getting Started

1. **Fork** the repository and clone it locally.
2. Create a new branch from `main` for your change:

   ```bash
   git checkout -b feat/your-feature-name
   ```

3. Make your changes, then commit with a clear message.
4. Push to your fork and **open a pull request** against `main`.

## Reporting Issues

- Search [existing issues](https://github.com/lowlydba/sustainable-npm/issues) before opening a new one.
- Include the Node.js version, runner OS, and a minimal reproducer when reporting bugs.

## Pull Request Guidelines

- Keep changes focused — one concern per PR.
- Update the [README](README.md) if your change affects documented behavior or inputs.
- Ensure the [test workflow](https://github.com/lowlydba/sustainable-npm/actions/workflows/test.yml) passes before requesting review.
- Follow the existing code style and YAML formatting conventions.

## Development

This action is implemented as a [composite action](https://docs.github.com/en/actions/sharing-automations/creating-actions/creating-a-composite-action) defined in [`action.yml`](action.yml). No build step is required — changes to `action.yml` take effect immediately.

To test locally against a real workflow, reference your fork branch directly:

```yaml
- uses: <your-fork>/sustainable-npm@<your-branch>
```

## Code of Conduct

Be respectful and constructive. Harassment or exclusionary behavior of any kind will not be tolerated.

## License

By contributing, you agree that your contributions will be licensed under the project's [MIT License](LICENSE).
