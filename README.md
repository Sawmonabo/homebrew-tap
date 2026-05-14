# Sawmonabo/homebrew-tap

A personal Homebrew tap for tools maintained by [@Sawmonabo](https://github.com/Sawmonabo).

## Usage

```bash
brew tap Sawmonabo/tap
brew install <formula-name>
```

Homebrew strips the `homebrew-` prefix when resolving `brew tap Sawmonabo/tap`, so this repo's name (`homebrew-tap`) is required for the short syntax to work.

## Formulas

| Formula | Description | Upstream |
|---|---|---|
| [`sidekick-usages`](./Formula/sidekick-usages.rb) | Check Claude Code and Codex CLI usage across multiple accounts in one command. | [Sawmonabo/sidekick-usages](https://github.com/Sawmonabo/sidekick-usages) |

## Install one of them

```bash
brew tap Sawmonabo/tap
brew install sidekick-usages
```

## CI status

[![Test formula](https://github.com/Sawmonabo/homebrew-tap/actions/workflows/test-formula.yml/badge.svg)](https://github.com/Sawmonabo/homebrew-tap/actions/workflows/test-formula.yml)

Every push and PR runs `brew install --build-from-source` and `brew test` against each formula on macOS, so a green badge means the tap is currently installable.

## Updating a formula

Each tool's source repo owns the source-of-truth copy of the formula. To bump a version:

1. Tag the new release in the source repo (e.g. `git tag v0.2.0 && git push --tags` in `sidekick-usages`).
2. Compute the SHA256 of the auto-generated tarball:
   ```bash
   curl -sL https://github.com/Sawmonabo/sidekick-usages/archive/refs/tags/v0.2.0.tar.gz | shasum -a 256
   ```
3. Refresh Python `resource` blocks if dependencies changed:
   ```bash
   brew update-python-resources Formula/sidekick-usages.rb
   ```
4. Update `url`, `sha256`, and any version-pinned resources in `Formula/<name>.rb`.
5. Verify locally:
   ```bash
   brew install --build-from-source ./Formula/sidekick-usages.rb
   brew test sidekick-usages
   brew audit --strict Sawmonabo/tap/sidekick-usages
   ```
6. Open a PR. CI will repeat the install+test on a clean macOS runner.

## License

Apache-2.0. Individual formulas may package software under different licenses — see each formula's `license` field.
