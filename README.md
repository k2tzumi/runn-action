# runn-action

:octocat: GitHub Action for [runn](https://github.com/k1LoW/runn)

## Usage

Add scenario file to your repository.

And set up a workflow file as follows and run runn on GitHub Actions.

``` yaml
# .github/workflows/ci.yml
name: API scenario Test

on:
  push:
    branches:
      - main
  pull_request:

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      -
        uses: actions/checkout@v2
      -
        uses: k2tzumi/runn-action@v0
        with:
          path_pattern: testdata/path/to/*.yml
```

See [action.yml](action.yml) and [runn README](https://github.com/k1LoW/runn) for more details on how to runbook it.