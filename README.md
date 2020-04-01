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
      KUBECONFIG_SECRET: ${{ secrets.kubeconfig }}
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Fleet apply
      uses: StrongMonkey/flt-apply@v0.0.1
```

Note: you have to add base64 encoded kubeconfig that points to your fleet manager cluster as a github secret. To see how a secret can be added in github repo, check https://help.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets.

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


To check out these two github actions, go to https://github.com/marketplace/actions/fleet-apply and https://github.com/marketplace/actions/fleet-test. 
