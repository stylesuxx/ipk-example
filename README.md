# Example IPK builder and Release workflow
This repo is meant as an example regarding workflows and IPK's.

The `Makefile` is used to build an IPK from the available data. The workflow file is meant to create a new release as soon as a new tag is pushed to the repository. It will thus trigger building the IPK and attaching it to the release.

## Workflow
Check [automation.yml](./.github/workflows/automation.yml) this file should be pretty self explanatory, there are two jobs: **build** and **release**.

Both jobs run when something is pushed to master and when new tags are pushed. The **build** job runs the `Makefile` and creates the artifact. The release file fetches the artifact and makes a new release, attaching all available IPK files as assets to the new release.

When pushed to master the release will be marked as **pre-release**, only when a new tag is pushed it is marked as a full release.
