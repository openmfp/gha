# openMFP - Github Actions Reuse Workflows

[![REUSE status](
https://api.reuse.software/badge/github.com/openmfp/gha)](https://api.reuse.software/info/github.com/openmfp/gha)

## Description

This repository holds reusable gha workflow and pipeline definitions


## Getting started

Add a workflow to your repository like so:

```yaml
name: ci
on: [push]

# The reusable workflow needs these permissions on the caller's token.
# Under the default (read-only) permissions the pipeline fails on tag
# creation / version commits and on npm provenance when publishing.
permissions:
  contents: write # tag creation and version commits
  id-token: write # npm provenance when publishing

jobs:
  pipe:
    concurrency:
      group: ${{ github.ref }}
      cancel-in-progress: true
    uses: openmfp/gha/.github/workflows/pipeline-node-module.yml@main
    secrets:
      # Required to publish; omit it together with `publish: false` below
      # if your package is not published.
      OPENMFP_PUBLISHER_PRIVATE_KEY: ${{ secrets.OPENMFP_PUBLISHER_PRIVATE_KEY }}
    with:
      # The deployment environment that holds the publishing credentials.
      environment: npmjs:@openmfp/your-package
```

If the package is not published, drop the `secrets` block and the
`environment` input and disable publishing instead:

```yaml
jobs:
  pipe:
    uses: openmfp/gha/.github/workflows/pipeline-node-module.yml@main
    with:
      publish: false
```

## Releasing

The release is performed automatically by merging to the main branch, since the other repositories are using the workflows from there.


## Requirements

gha requires a GitHub fork with a pipeline, that is using the workflows, to validate the changes.

## Contributing

Please refer to the [CONTRIBUTING.md](CONTRIBUTING.md) file in this repository for instructions on how to contribute to openMFP.

## Code of Conduct

Please refer to the [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) file in this repository informations on the expected Code of Conduct for contributing to openMFP.

## Licensing

Copyright 2024 SAP SE or an SAP affiliate company and openMFP contributors. Please see our [LICENSE](LICENSE) for copyright and license information. Detailed information including third-party components and their licensing/copyright information is available [via the REUSE tool](https://api.reuse.software/info/github.com/openmfp/gha).



<p align="center"><img alt="Bundesministerium für Wirtschaft und Energie (BMWE)-EU funding logo" src="https://apeirora.eu/assets/img/BMWK-EU.png" width="400"/></p>
