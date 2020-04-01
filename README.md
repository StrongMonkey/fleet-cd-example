# Fleet Management github action example

This Repo serves as an example to use fleet manager as github action in CI.

You should have your bundle files defined in this repo. Then add workflows to your repo.

For example, to automatically apply your bundle into your fleet cluster, create `./github/workflows/push.yaml` workflow:

```yaml
name: push
on:
  push:
    branches: [ master ]

jobs:
  apply:
    env:
      KUBECONFIG: ${{ secrets.kubeconfig }}
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Fleet apply
      uses: StrongMonkey/flt-apply@v0.0.1
```

To automatically test if your bundle files are valid on any pull request, create `./github/workflows/pull.yaml` workflow:

```yaml
name: pull-request
on:
  pull_request:
    branches: [ master ]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Fleet test
      uses: StrongMonkey/flt-test@v0.0.1
```
