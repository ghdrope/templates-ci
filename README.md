# templates-ci

Using [Renovate](https://www.mend.io/renovate/) in my projects brought a lot of repetitive merge requests, since the CI workflows were all set up the same way.

`templates-ci` keeps those workflows in one place as reusable templates, so there is less to maintain and one place to look when something breaks.

## Why `main`

Calling the templates by a version tag would just move the problem: Renovate would open MRs to bump the `templates-ci` reference instead. So projects call the templates with `@main`.

## Templates

- `go-feat_ci_push.yml`: tidy check, lint, format check, unit tests
- `go-sast.yml`: CodeQL and govulncheck
- `go-dev_binary_publish.yml` / `go-binary_publish.yml`: dev / release binaries
- `docker-docker_dev.yml` / `docker-docker_publish.yml`: dev / release images
- `helm-feat_cd_push.yml`: Helm lint and template

## Usage Examples

- Single component: [wis2-ingest](https://github.com/ghdrope/wis2-ingest/tree/1.5.8/.github/workflows)
- Multi component: [court](https://github.com/ghdrope/court/tree/0.0.16/.github/workflows)
