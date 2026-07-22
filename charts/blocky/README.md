# blocky

![Version: 0.1.0](https://img.shields.io/badge/Version-0.1.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: v0.33.0](https://img.shields.io/badge/AppVersion-v0.33.0-informational?style=flat-square)

Fast and lightweight DNS proxy as ad-blocker for local network with many features

## TL;DR

```console
helm install blocky ./charts/blocky
```

## Prerequisites

* Kubernetes 1.19+

## Installing the Chart

To install the chart with the release name `blocky`:

```console
helm install blocky ./charts/blocky
```

## Uninstalling the Chart

To uninstall/delete the `blocky` deployment:

```console
helm uninstall blocky
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example:

```console
helm install blocky \
  --set replicaCount=2 \
  ./charts/blocky
```

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart:

```console
helm install blocky -f values.yaml ./charts/blocky
```

## Source Code

* <https://github.com/0xERR0R/blocky>

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` | Node affinity rules for pod assignment |
| config | object | `{"blocking":{"clientGroupsBlock":{"default":["ads"]},"denylists":{"ads":["https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts"]}},"ports":{"dns":5553,"http":4000},"prometheus":{"enable":true,"path":"/metrics"},"upstreams":{"groups":{"default":["1.1.1.1","1.0.0.1","https://cloudflare-dns.com/dns-query"]}}}` | Native Blocky configuration object (automatically converted to YAML and mounted to config.yml) |
| fullnameOverride | string | `""` | Override the full chart name |
| image.pullPolicy | string | `"IfNotPresent"` | Image pull policy |
| image.repository | string | `"ghcr.io/0xerr0r/blocky"` | Container image repository |
| image.tag | string | `""` | Overrides the image tag whose default is the chart appVersion |
| imagePullSecrets | list | `[]` | Image pull secrets for private registries |
| ingress.annotations | object | `{}` | Annotations for the ingress |
| ingress.className | string | `""` | Ingress Class Name |
| ingress.enabled | bool | `false` | Enable ingress controller resource |
| ingress.hosts | list | `[{"host":"blocky.local","paths":[{"path":"/","pathType":"ImplementationSpecific"}]}]` | Ingress host configurations |
| ingress.tls | list | `[]` | Ingress TLS configuration |
| livenessProbe | object | `{"httpGet":{"path":"/","port":"http"}}` | Liveness probe configuration |
| nameOverride | string | `""` | Override the chart name |
| nodeSelector | object | `{}` | Node selector labels for pod assignment |
| openshift | bool | `false` | Enable extra platform features |
| persistence | object | `{"cache":{"accessMode":"ReadWriteOnce","enabled":false,"existingClaim":"","size":"1Gi","storageClass":""},"logs":{"accessMode":"ReadWriteOnce","enabled":false,"existingClaim":"","size":"5Gi","storageClass":""}}` | Persistence configuration for cache and logs directories |
| persistence.cache.accessMode | string | `"ReadWriteOnce"` | Access mode for cache PVC |
| persistence.cache.enabled | bool | `false` | Enable persistent volume claim for cache directory (defaults to false using emptyDir) |
| persistence.cache.existingClaim | string | `""` | Use an existing PVC for cache |
| persistence.cache.size | string | `"1Gi"` | Size of cache volume |
| persistence.cache.storageClass | string | `""` | Storage class for cache PVC |
| persistence.logs.accessMode | string | `"ReadWriteOnce"` | Access mode for query logs PVC |
| persistence.logs.enabled | bool | `false` | Enable persistent volume claim for query logs directory (defaults to false using emptyDir) |
| persistence.logs.existingClaim | string | `""` | Use an existing PVC for query logs |
| persistence.logs.size | string | `"5Gi"` | Size of query logs volume |
| persistence.logs.storageClass | string | `""` | Storage class for query logs PVC |
| podAnnotations | object | `{}` | Annotations for the blocky pod |
| podLabels | object | `{}` | Labels for the blocky pod |
| podSecurityContext | object | `{"runAsNonRoot":true,"seccompProfile":{"type":"RuntimeDefault"}}` | Pod security context settings |
| readinessProbe | object | `{"httpGet":{"path":"/","port":"http"}}` | Readiness probe configuration |
| replicaCount | int | `1` | Number of replicas for the deployment |
| resources | object | `{}` | CPU/Memory resource requests and limits |
| route.enabled | bool | `false` | Enable Route resource |
| route.host | string | `"blocky.apps.example.com"` | Hostname for the Route |
| route.tls | object | `{"insecureEdgeTerminationPolicy":"Redirect","termination":"edge"}` | TLS configuration for Route |
| securityContext | object | `{"allowPrivilegeEscalation":false,"capabilities":{"drop":["ALL"]},"readOnlyRootFilesystem":true,"runAsNonRoot":true}` | Container security context settings |
| service.annotations | object | `{}` | Service annotations |
| service.dnsPort | int | `5553` | Port for DNS queries (UDP and TCP) |
| service.httpPort | int | `4000` | Port for HTTP web server and Prometheus metrics |
| service.type | string | `"ClusterIP"` | Kubernetes Service type |
| serviceAccount.annotations | object | `{}` | Annotations to add to the service account |
| serviceAccount.create | bool | `true` | Specifies whether a service account should be created |
| serviceAccount.name | string | `""` | The name of the service account to use. If not set and create is true, a name is generated using the fullname template |
| serviceMonitor.enabled | bool | `false` | Enable Prometheus ServiceMonitor resource |
| serviceMonitor.interval | string | `"30s"` | Prometheus scrape interval |
| serviceMonitor.scrapeTimeout | string | `"10s"` | Prometheus scrape timeout |
| tolerations | list | `[]` | Node tolerations for pod assignment |

## Changelog

### 0.1.0

* Initial release of the Blocky Helm chart.

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
