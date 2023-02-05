# Example IPK builder and Release workflow
This repo is meant as an example regarding workflows and IPKs.

The `Makefile` is used to build an IPK from the available `control` and `data` directories. The `automation.yml` workflow file is meant to create a new release as soon as a new tag is pushed to the repository.

> It will thus trigger building the IPK, create a release and attaching the IPK to it.

## Control
The `control` directory contains the `control` file, which is used to define the package name, version, maintainer, dependencies and so on.
the `Architecture` field can have the following values:
- `all` - the package is architecture independent
- `pigeon-all` - all pigeon architectures
- `pigeon-glasses` - only goggles
- `pigeon-glasses-v1` - only goggles v1
- `pigeon-glasses-v2` - only goggles v2
- `pigeon-airside` - only airside
- `pigeon-airside-au` - only air units
- `pigeon-airside-lite` - only vistas
- `armv7-3.2` - the package is only for the armv7 architecture

## Workflow
Check [automation.yml](./.github/workflows/automation.yml) this file should be pretty self explanatory, there are two jobs: **build** and **release**.

Both jobs run when something is pushed to master and when new tags are pushed. The **release** job `needs` the **build** job, so it runs first.

It basically runs the `Makefile` and creates the artifact. The release job fetches the artifact and generates a new release, attaching all available IPK files as assets to the new release.

## Tagging
When pushed to master the release will be marked as **pre-release**, only when a new tag is pushed it is marked as a full release, the tag name will then also be the releases name.
