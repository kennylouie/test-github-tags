# Github Workflow for Docker Build and Release

## Design

In the `.github/workflows` folder, there are 3 workflows that can be used as a cicd for docker build and release.

### `tests.yml`

This workflow is for PRs. This is used to run tests. The only *requirements* are:

1. a semantic versioning is used for every PR. For e.g. `origin/master` needs to be set with a `v0.0.1` tag.

2. Subsequent PRs will need to increment the tag, e.g. `v0.0.2`. 

The `tests.yml` workflow will check that the tag is incremented.

### `docker-dev.yml`

This workflow is for merges to master. Assuming that the `tests.yml` workflow has checked PRs, the merge to master will build and tag according to `origin/master`'s tag e.g. `name/image-name:0.0.1`. This will also produce a corresponding `name/image-name:latest`. Both tags use the latest commit from master.

### `docker-prod.yml`

This workflow will check a new release and use the version in that release tag and push as `name/image-name:prod`.
