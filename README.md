# GitHub Action: `setup-sentinel`

The `hashicorp/setup-sentinel` Action sets up the [Sentinel](https://www.hashicorp.com/sentinel) CLI in your GitHub Actions workflow by adding the `sentinel` binary to `PATH`.

[![GitHub Action: Self-Test](https://github.com/hashicorp/setup-sentinel/actions/workflows/actions-self-test.yml/badge.svg?branch=main)](https://github.com/hashicorp/setup-sentinel/actions/workflows/actions-self-test.yml)

## Table of Contents

<!-- TOC -->
* [GitHub Action: `setup-sentinel`](#github-action-setup-sentinel)
  * [Table of Contents](#table-of-contents)
  * [Requirements](#requirements)
  * [Usage](#usage)
  * [Inputs](#inputs)
  * [Outputs](#outputs)
  * [License](#license)
<!-- TOC -->

## Requirements

This GitHub Actions supports all commands that are available in the `sentinel` CLI.

## Usage

Create a GitHub Actions Workflow file (e.g.: `.github/workflows/sentinel.yml`):

```yaml
name: sentinel

on:
  push:

env:
  PRODUCT_VERSION: "0.25.1" # or: "latest"

jobs:
  sentinel:
    runs-on: ubuntu-latest
    name: Run Sentinel
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup `sentinel`
        uses: hashicorp/setup-sentinel@main
        id: setup
        with:
          version: ${{ env.PRODUCT_VERSION }}

      - name: Run `sentinel init`
        id: init
        run: "sentinel test"
```

In the above example, the following definitions have been set.

- The event trigger has been set to `push`. For a complete list, see [Events that trigger workflows](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows).
- The origin of this GitHub Action has been set as `hashicorp/setup-sentinel@main`. For newer versions, see the [Releases](https://github.com/hashicorp/setup-sentinel/releases).
- The version of `sentinel` to set up has been set as `0.25.1`. For a complete list, see [releases.hashicorp.com](https://releases.hashicorp.com/sentinel/).

These definitions may require updating to suit your deployment, such as specifying [self-hosted](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#choosing-self-hosted-runners) runners.

Additionally, you may configure [outputs](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#example-defining-outputs-for-a-job) to consume return values from the Action's operations.

## Inputs

This section contains a list of all inputs that may be set for this Action.

- `version` - The version of `sentinel` to install. Defaults to `latest` if unset.

> [!NOTE]
> To retrieve the `latest` version, this GitHub Action polls the HashiCorp [Releases API](https://api.releases.hashicorp.com/v1/releases/sentinel) and finds the latest released version of sentinel that isn't marked as a pre-release (`is_prerelease`).

## Outputs

This section contains a list of all outputs that can be consumed from this Action.

- `version` -  The version of `sentinel` that was installed.

## License

Licensed under the Apache License, Version 2.0 (the "License").

You may obtain a copy of the License at [apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0).

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an _"AS IS"_ basis, without WARRANTIES or conditions of any kind, either express or implied.

See the License for the specific language governing permissions and limitations under the License.
