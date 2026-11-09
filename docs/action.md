# GitHub Action

The action runs `compose-rot check` on your repo and fails the step when it finds something.

```yaml
name: compose-rot
on:
  push:
  schedule:
    - cron: "0 3 * * 1"

jobs:
  scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v7
      - uses: kd-011/compose-rot@v0
        with:
          paths: stacks
```

Run it on a schedule as well as on push. The data file grows as upstreams change, so a stack that was clean last month can have a finding today.

## Inputs

| Input | Default | What it does |
| --- | --- | --- |
| `paths` | `.` | Files or directories to scan, separated by spaces. |
| `online` | `false` | Ask the registry and GitHub about each image's upstream. |
| `github-token` | `github.token` | Token for the GitHub API in online mode. |
| `ignore` | empty | Images to skip, separated by spaces. |
| `exclude` | empty | Directory names to skip, separated by spaces. |

The step exits 1 when there are findings and 2 when a file cannot be read, the same as the command line.
