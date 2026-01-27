# Axelix Kubernetes Helm Chart

[![License](https://img.shields.io/badge/license-MIT-blue)](https://opensource.org/license/mit)
[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/axelix)](https://artifacthub.io/packages/search?repo=axelix)

The code is provided as-is with no warranties.

# How We Manage and Release Charts

Because we want our helm charts to be:

- Discoverable via `helm repo add axelixlabs https://axelixlabs.github.io/helm-charts`
- Discoverable on the Helm Artifacts Hub

We're releasing our charts in the following way:

1. In the GitHub Pages (`gh-pages` branch), we have the `index.yaml` that serves as the main index file for the `helm search` CLI commands (Assuming the repository was added).
2. GitHub Pages also serve as the actual repository URL for the Artifacts Hub, since it hosts the `index.yaml` along the `artifacthub-repo.yml`.
3. The actual helm charts are released as compressed tarballs (`.tgz`) inside the GitHub Releases, i.e. each released artifact is bound to a particular GitHub release. The GitHub release page [can be found here](https://github.com/axelixlabs/helm-charts/releases). 

## Usage

[Helm](https://helm.sh) must be installed to use the charts.
Please refer to Helm's [documentation](https://helm.sh/docs/) to get started.

Once Helm is set up properly, add the repo as follows:

```console
helm repo add axelixlabs https://axelixlabs.github.io/helm-charts
```

You can then run `helm search repo axelix` to find the chart.

Chart documentation is available in [axelix directory](https://github.com/axelixlabs/helm-charts/blob/main/charts/axelix/README.md).

## Contributing

We'd love to have you contribute! Please refer to our [contribution guidelines](https://github.com/axelixlabs/helm-charts/blob/main/CONTRIBUTING.md) for details.

## License

[MIT License](https://github.com/axelixlabs/helm-charts/blob/main/LICENSE).