# install-aws-cli-action

Install AWS CLI on a GitHub Actions Linux host. 

After this action, every step is capable of running `aws` CLI, and it's up to you to set the environment variables (secrets) `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.

## Usage

Valid `version` values:

- `1` - latest v1
- `2` - latest v2 (default)
- `1.##.##` - specific v1
- `2.##.##` - specific v2

### Snippet

Add the following step to a job in your workflow

```yaml
- id: install-aws-cli
  uses: kuju63/setup-aws-cli@v1.1.0
  with:
    version: 2 # default
    verbose: false # default
    http_proxy: "" # default
    https_proxy: "" # default
```

### Full example

```yaml
on: [push]

jobs:
  test_no_input:
    runs-on: ubuntu-latest
    name: no input
    steps:
      - uses: actions/checkout@v2
      - id: install-aws-cli
        uses: kuju63/setup-aws-cli@v1.1.0
      - run: aws --version
        shell: bash

  test_latest_version_v1:
    runs-on: ubuntu-latest
    name: latest v1
    steps:
      - uses: actions/checkout@v2
      - id: install-aws-cli
        uses: kuju63/setup-aws-cli@v1.1.0
        with:
          version: 1
      - run: aws --version
        shell: bash

  test_latest_version_v2:
    runs-on: ubuntu-latest
    name: latest v2
    steps:
      - uses: actions/checkout@v2
      - id: install-aws-cli
        uses: kuju63/setup-aws-cli@v1.1.0
        with:
          version: 2
      - run: aws --version
        shell: bash

  test_specific_v1:
    runs-on: ubuntu-latest
    name: specific v1
    steps:
      - uses: actions/checkout@v2
      - id: install-aws-cli
        uses: kuju63/setup-aws-cli@v1.1.0
        with:
          version: 1.18.1
      - run: aws --version
        shell: bash

  test_specific_v2:
    runs-on: ubuntu-latest
    name: specific v2
    steps:
      - uses: actions/checkout@v2
      - id: install-aws-cli
        uses: kuju63/setup-aws-cli@v1.1.0
        with:
          version: 2.0.30
      - run: aws --version
        shell: bash
  test_on_proxy:
    runs-on: ubuntu-latest
    name: on proxy
    steps:
      - uses: actions/checkout@v2
      - id: install-aws-cli
        uses: kuju63/setup-aws-cli@v1.1.0
        with:
          version: 2.0.30
          http_proxy: ${{ secrets.HTTP_PROXY }}
          https_proxy: ${{ secrets.HTTPS_PROXY }}
      - run: aws --version
        shell: bash
```
