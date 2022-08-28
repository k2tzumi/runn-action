# runn-action

:octocat: GitHub Action for [runn](https://github.com/k1LoW/runn)

## Usage

Add scenario file to your repository.

And set up a workflow file as follows and run runn on GitHub Actions.

The actions of the runn command are executed in the container.

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
    services:
      httpbin:
        image: kennethreitz/httpbin:latest
        ports:
          - 8080:80
    steps:
      -
        uses: actions/checkout@v2
      -
        uses: k2tzumi/runn-action@v0
        with:
          path_pattern: testdata/path/to/*.yml
        env:
          # Override parameters in scenario with environment variables
          # NOTE: Specify `172.17.0.1` when accessing services on the GitHub Actions host.
          END_POINT: http://172.17.0.1:8080/
```

See [action.yml](action.yml) and [runn README](https://github.com/k1LoW/runn) for more details on how to runbook it.