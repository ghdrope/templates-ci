# ci-templates

The integration of [Renovate](https://www.mend.io/renovate/) in the projects bring along a series of merge requests (MRs). These turn out to be repetitive as the CI workflows were setup similarly, leading to frequent repetitive maintaining tasks in each of the repositories.

`ci-templates` centralized now the used workflows as callable templates. It reduces effort to maintain, and acts a single point for troubleshooting reference.

## The Latest Tag

Calling the templates through the available semantic versioning tag would keep the before mentioned problem happening. Renovate MRs would stop addressing directly dependency updates, but would turn out to be for `ci-templates` reference.

To deal with this calling repositories should use the reference `latest`.

### Recreate `latest`

Every time a new release is created `latest` tag should be recreated.

## Usage Examples

### Single Component Project

- [wis2-ingest Workflows](https://github.com/ghdrope/wis2-ingest/tree/1.5.8/.github/workflows)

### Multi Component Project

- [Court Workflows](https://github.com/ghdrope/court/tree/0.0.16/.github/workflows)
