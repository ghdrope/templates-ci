# templates-ci

Using [Renovate](https://docs.renovatebot.com/) in my projects brought a lot of repetitive pull requests, since the CI workflows were all set up the same way.

`templates-ci` keeps those workflows in one place as reusable templates, so there is less to maintain and one place to look when something breaks.

## Why `main`

Calling the templates by a version tag would just move the problem: Renovate would open pull requests to bump the `templates-ci` reference instead. So projects call the templates with `@main`.

The trade-off is that a broken template breaks every project at once. To catch that early, every change here is checked with [actionlint](https://github.com/rhysd/actionlint) and [zizmor](https://github.com/zizmorcore/zizmor) before it reaches `main`.

## Templates

- `go-feat_ci_push.yml`: tidy check, lint, format check, unit tests
- `go-sast.yml`: CodeQL and govulncheck
- `go-dev_binary_publish.yml` / `go-binary_publish.yml`: dev / release binaries
- `docker-docker_dev.yml` / `docker-docker_publish.yml`: dev / release images for `linux/amd64` and `linux/arm64`, with SBOM and provenance on release
- `helm-feat_cd_push.yml`: Helm lint and template

## Usage

```yaml
jobs:
  ci:
    uses: ghdrope/templates-ci/.github/workflows/go-feat_ci_push.yml@main
```

The templates call `make` targets, so the project needs them in its Makefile: `lint`, `format-check`, `test-unit`, `check-vulnerability`, `build` (or `build-all` for multi-component projects), and `helm-lint` / `helm-template` for Helm charts.

Examples:

- Single component: [wis2-ingest](https://github.com/ghdrope/wis2-ingest/tree/1.5.8/.github/workflows)
- Multi component: [court](https://github.com/ghdrope/court/tree/0.0.16/.github/workflows)
