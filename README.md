# app-wfa

GitHub workflow actions

## How to use

reference: https://docs.github.com/en/actions/using-workflows/reusing-workflows

### Appinspect

Example configuration

``` yml
name: Splunk Appinspect
on:
  pull_request:
    branches:
      - main
      - master
    paths:
      - "src/**"
    types: [opened, ready_for_review]
  workflow_dispatch:

jobs:
  call-packaging-workflow:
    uses: ZachTheSplunker/app-wfa/.github/workflows/appinspect.yml@main
    secrets: inherit
    with: 
        package-name: Package-name
```