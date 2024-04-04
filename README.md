## Description

This repository holds reusable gha workflow and pipeline definitions


## Getting started

Add a workflow to your repository like so:

```
name: ci
on: [push]

jobs:
  pipe:
    concurrency:
      group: ${{ github.ref }}
      cancel-in-progress: true
    uses: openmfp/gha/.github/workflows/pipeline-golang-module.yml@main
    secrets: inherit
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

Copyright 2024 SAP SE or an SAP affiliate company and openMFP contributors. Please see our [LICENSE](LICENSE) for copyright and license information. Detailed information including third-party components and their licensing/copyright information is available [via the REUSE tool](https://api.reuse.software/info/github.com/openmfp/golang-commons).