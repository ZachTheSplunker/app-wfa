# app-wfa

GitHub workflow actions

## How to use

reference: https://docs.github.com/en/actions/using-workflows/reusing-workflows

### Appinspect Example

Required Input | Description
-------------- | -----------
API_USER | splunkbase username defined as secret
API_PASS | splunkbase password defined as secret
package-name | name of app package

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
    secrets:
      API_USER: ${{ secrets.API_USER }}
      API_PASS: ${{ secrets.API_PASS }}
```

### Release Example

Required Input | Description
-------------- | -----------
package-name | name of app package

``` yml
name: release
on:
  workflow_dispatch:
  push:
    branches:
      - master
      - main
    paths:
      - "Package-name/**"

jobs:
  call-packaging-workflow:
    uses: ZachTheSplunker/app-wfa/.github/workflows/release.yml@main
    with:
      package-name: Package-name
```

### Docs Example

``` yml
name: docs

on:
  workflow_dispatch:
  push:
    branches:
      - main
      - master
    paths:
      - "docs/**"

jobs:
  call-packaging-workflow:
    uses: ZachTheSplunker/app-wfa/.github/workflows/docs.yml@main
```