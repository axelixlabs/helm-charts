# Axelix Helm Chart

* Installs [Axelix Master](https://github.com/axelixlabs/axelix) to Kubernetes, deploying the Axelix Master component.

## Get Repo Info

```console
helm repo add axelixlabs https://axelixlabs.github.io/helm-charts
helm repo update
```

_See [helm repo](https://helm.sh/docs/helm/helm_repo/) for command documentation._

## Installing the Chart

To install the chart with the release name `my-release`:

```console
helm install my-release axelixlabs/axelix
```

The command deploys Axelix Master on the Kubernetes cluster with the default configuration. The [Configuration](#configuration) section lists the parameters that can be configured during installation.

## Uninstalling the Chart

To uninstall/delete the my-release deployment:

```console
helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the Axelix Master chart and their default values.

{{ template "chart.valuesTable" . }}

## Installing the Chart with Custom Values

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example:

```console
helm install my-release axelixlabs/axelix \
  --set image.name=myregistry/axelix \
  --set image.ref=v1.0.0 \
```

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example:

```console
helm install my-release axelixlabs/axelix -f values.yaml
```

## App Configuration

By default, axelix-master container runs on port 8080 and handles both API endpoints and the UI. The service is exposed at `/` path when ingress is enabled.

### Health Checks

The axelix-master includes health check endpoints:
- Liveness: `/api/axelix/actuator/health/liveness`
- Readiness: `/api/axelix/actuator/health/readiness`

## Ingress Configuration

When `ingress.enabled` is set to `true`, the chart creates an Ingress resource that routes traffic to the axelix-master service (port 8080). By default, the ingress is created in the same namespace as the release. You can override this by setting `ingress.namespace`.

### Example Ingress Configuration

```yaml
ingress:
  enabled: true
  className: nginx
  host: axelix.example.com
  annotations:
    cert-manager.io/cluster-issuer: "letsencrypt-prod"
  tls:
    enabled: true
    secretName: axelix-tls
```

## Service Accounts and RBAC

The chart can create a service account for the axelix-master component. By default, the service account is created in the same namespace as the release. You can override this by setting `serviceAccount.namespace`.

The service account can be granted permissions via RBAC to access Kubernetes resources.

### RBAC Configuration

When `rbac.autoCreateRole` is enabled, the chart creates:
- A `Role` in the `rbac.targetNamespace` with permissions to get, list, and watch pods, services, and endpoints
- A `RoleBinding` that binds the axelix-master service account to the role

This allows axelix-master to monitor Kubernetes resources in the specified namespace. Note that `rbac.targetNamespace` can be different from the release namespace if you want to monitor resources in a different namespace.

## Resource Management

The axelix-master supports custom resource requests and limits. Configure resources as follows:

```yaml
resources:
  requests:
    memory: "256Mi"
    cpu: "100m"
  limits:
    memory: "512Mi"
    cpu: "500m"
```

## Node Selection and Scheduling

You can control pod placement using node selectors, affinity rules, and tolerations:

```yaml
nodeSelector:
  kubernetes.io/os: linux

affinity:
  podAntiAffinity:
    preferredDuringSchedulingIgnoredDuringExecution:
    - weight: 100
      podAffinityTerm:
        labelSelector:
          matchExpressions:
          - key: app.kubernetes.io/name
            operator: In
            values:
            - axelix-master
        topologyKey: kubernetes.io/hostname

tolerations:
- key: "special"
  operator: "Equal"
  value: "true"
  effect: "NoSchedule"
```

## Volumes and Volume Mounts

The axelix-master supports additional volumes and volume mounts:

```yaml
volumes:
- name: config
  configMap:
    name: axelix-master-config

volumeMounts:
- name: config
  mountPath: /etc/axelix/config
  readOnly: true
```

## Image Configuration

Configure the container image:

```yaml
image:
  name: "ghcr.io/axelixlabs/axelix"
  ref: "1.0.0"
  pullPolicy: "IfNotPresent"
```

### Image Pull Secrets

If your images are in a private registry, configure image pull secrets:

```yaml
imagePullSecrets:
  - name: myregistry-secret
```
