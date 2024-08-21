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
        uses: actions/checkout@v4
      -
        uses: k2tzumi/runn-action@latest
        with:
          path_pattern: testdata/path/to/*.yml
        env:
          # Override parameters in scenario with environment variables
          # NOTE: Specify `172.17.0.1` when accessing services on the GitHub Actions host.
          END_POINT: http://172.17.0.1:8080/
```

# Action parameters

- `command`  
`Required` `run` a scenario by specifying run.  
`list` the contents of a scenario by specifying list.  
If `loadt` is specified, the scenario can be used as a load test. 
Default is `run`.
- `path_pattern`  
`Required` Specify the path to the Runbook ( runn scenario file ).
- `debug`  
Enable runtime debug output. Default is `false`.
- `verbose`  
Enable detailed progress output. Default is `false`.
- `version`  
This parameter specifies the version of runn.  
If this parameter is omitted, runn-action automatically selects and runs the same version of runn as its own version.
- `fail-fast`  
Terminates the process if a step in the scenario fails in the middle of a step. Default is `false`.
- `skip-test`  
Scenario runs, but test is not evaluated. Default is `false`.
- `shuffle`  
Shuffle multiple Runbooks to run with the runn command. Default is `false`.
- `concurrent`  
Enable concurrent execution. Default is `false`.
- `enable-read-remote-scope`  
Enable `read:remote` scope. Default is `false`.
- `enable-run-exec-scope`  
Enable `run:exec` scope. Default is `false`.
- `labels`  
Specify a label to narrow down the target of execution. Multiple labels can be separated by commas.

See [action.yml](action.yml) and [runn README](https://github.com/k1LoW/runn) for more details on how to runbook it.
