(If anyone stumbles upon this file, it's just some notes for myself because I always forgor stuff)

### One-time GitHub setup

Configure trusted publishing for the release workflow:

* PyPI project `HyFetch`: trust this repository and `.github/workflows/release.yml`
* npm package `neowofetch`: trust this repository and `.github/workflows/release.yml`

No PyPI or npm API token secrets are needed. The publish jobs request GitHub's
OIDC token with `id-token: write`, and the registries exchange that token through
their trusted publishing flows.

### Things to do before deploying

* [ ] Update changelog (`README.md`) and commit changes
* [ ] Run `python -m tools.deploy-release {version}`
* [ ] Watch the `Release` workflow

The local script prepares the release commit and pushes the version tag. GitHub
Actions creates/completes the GitHub Release, uploads Python artifacts, publishes
to PyPI, and publishes to npm.

If the workflow fails after one stage already published, fix the problem and
rerun it. If the fix changes the workflow itself, run the workflow manually with
the same tag. The workflow checks PyPI, npm, and the GitHub Release first, so it
will skip completed stages instead of publishing them again.
