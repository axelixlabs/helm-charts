# Axelix Kubernetes Helm Chart

> [!IMPORTANT]
> **This repository is archived and no longer maintained.**
>
> The Axelix Helm chart has moved into the [axelixlabs/axelix](https://github.com/axelixlabs/axelix) monorepo
> (see [`charts/axelix`](https://github.com/axelixlabs/axelix/tree/main/charts/axelix)). Since all Axelix components
> are released in lockstep, the chart is now versioned and published as part of the single Axelix GitHub release,
> which also makes the overall management simpler.
>
> Please report issues and open pull requests in [axelixlabs/axelix](https://github.com/axelixlabs/axelix).

[![License](https://img.shields.io/badge/license-MIT-blue)](https://opensource.org/license/mit)
[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/axelix)](https://artifacthub.io/packages/search?repo=axelix)

## Migrating to the New Helm Repository

New chart versions are published to the `https://axelixlabs.github.io/axelix` Helm repository.
The old `https://axelixlabs.github.io/helm-charts` repository will not receive any new chart versions.

Replace the old repository with the new one:

```console
helm repo remove axelixlabs
helm repo add axelix https://axelixlabs.github.io/axelix
helm repo update
```

And install (or upgrade) the chart from it:

```console
helm upgrade --install axelix axelix/axelix
```

The full set of configurable properties is documented on the chart's [Artifact Hub page](https://artifacthub.io/packages/helm/axelix/axelix).

## License

This chart is available under [MIT License](https://github.com/axelixlabs/helm-charts/blob/main/LICENSE).
