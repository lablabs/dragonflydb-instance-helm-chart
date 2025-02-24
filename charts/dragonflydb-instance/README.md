# dragonflydb-instance

A Helm chart for deploying DragonflyDB databases using the DragonflyDB Operator CRD.

![Version: 0.1.0](https://img.shields.io/badge/Version-0.1.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.0.0](https://img.shields.io/badge/AppVersion-1.0.0-informational?style=flat-square)

## About
dragonflydb-instance Helm chart

## Requirements
- **cert-manager**: Required for managing TLS certificates.
  - Repository: [https://charts.jetstack.io](https://charts.jetstack.io)

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| acl | object | `{"enabled":true,"existingSecret":"","key":"","optional":false,"rules":""}` | Access Control List (ACL) configuration |
| acl.enabled | bool | `true` | Enable ACL |
| acl.rules | string | `""` | The ACL rules to apply to the database if existingSecret is empty @see https://www.dragonflydb.io/docs/managing-dragonfly/acl Example: rules: |   user user on >pass ~* &* +@string +@fast -@slow +set   user rouser on >ropass ~* &* +@read |
| affinity | object | `{}` | Affinity rules for pod assignment @see https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity |
| args | list | `[]` | DragonflyDB configuration flags @see https://www.dragonflydb.io/docs/managing-dragonfly/flags |
| authentication | object | `{"password":{"enabled":false,"existingSecret":"","key":"","optional":false,"password":""},"tls":{"enabled":false,"optional":false}}` | Authentication configuration for DragonflyDB Only one type of authentication can be enabled at a time. If both password.enabled and tls.enabled are set to true, the deployment will fail. |
| authentication.password | object | `{"enabled":false,"existingSecret":"","key":"","optional":false,"password":""}` | Password-based authentication configuration |
| authentication.password.enabled | bool | `false` | Enable password authentication |
| authentication.password.existingSecret | string | `""` | Name of existing secret containing the password If empty, a new secret will be created |
| authentication.password.key | string | `""` | The key to use for the password in the secret |
| authentication.password.optional | bool | `false` | Optional password authentication |
| authentication.password.password | string | `""` | Password to use when existingSecret is empty |
| authentication.tls | object | `{"enabled":false,"optional":false}` | TLS-based client authentication configuration |
| authentication.tls.enabled | bool | `false` | Enable TLS client authentication |
| authentication.tls.optional | bool | `false` | Optional TLS client authentication |
| fullnameOverride | string | `""` | String to fully override app.fullname template |
| labels | object | `{}` | Additional labels to add to all resources XXX |
| nameOverride | string | `""` | String to partially override app.fullname template |
| nodeSelector | object | `{}` | Node selector for pod assignment @see https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector |
| pdb | object | `{"enabled":false,"maxUnavailable":0,"minAvailable":0}` | Pod disruption budget configuration @see https://kubernetes.io/docs/tasks/run-application/configure-pdb/ |
| pdb.enabled | bool | `false` | Enable pod disruption budget |
| pdb.maxUnavailable | int | `0` | Maximum number of pods that can be unavailable |
| pdb.minAvailable | int | `0` | Minimum number of pods that must be available |
| podMonitor | object | `{"enabled":false,"endpoints":[{"port":"admin"}]}` | Prometheus PodMonitor configuration |
| podMonitor.enabled | bool | `false` | Enable Prometheus PodMonitor |
| podMonitor.endpoints | list | `[{"port":"admin"}]` | Define how to scrape metrics from the selected pod |
| priorityClassName | string | `""` | Priority class name for pods @see https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/ |
| replicas | int | `1` | Number of DragonflyDB replicas to deploy |
| resources | object | `{}` | Resource requests and limits for the DragonflyDB pods |
| serviceAccount | object | `{"annotations":{},"create":true,"name":""}` | Service account configuration |
| serviceAccount.annotations | object | `{}` | Annotations to add to the service account |
| serviceAccount.create | bool | `true` | Specifies whether a service account should be created |
| serviceAccount.name | string | `""` | The name of the service account to use If not set and create is true, a name is generated using the fullname template |
| snapshot | object | `{"cron":"* * * * *","dir":"","enabled":false}` | Configuration for snapshot functionality |
| snapshot.cron | string | `"* * * * *"` | Cron expression to define the schedule for taking snapshots |
| snapshot.dir | string | `""` | Destination directory for storing snapshots This can be an S3 bucket URL `s3://<bucket-name>/` or a local directory path. |
| snapshot.enabled | bool | `false` | Enable or disable periodic snapshots |
| tls | object | `{"enabled":false,"existingSecret":""}` | TLS configuration for the server |
| tls.enabled | bool | `false` | Enable TLS for the server. Note: If TLS is enabled, at least one authentication method (password or TLS) must be configured. |
| tls.existingSecret | string | `""` | Name of existing secret containing the TLS certificates The secret should contain: - tls.crt: The server certificate - tls.key: The private key - ca.crt: The CA certificate |
| tolerations | list | `[]` | Tolerations for pod assignment @see https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/ |
| topologySpreadConstraints | list | `[]` | Pod topology spread constraints @see https://kubernetes.io/docs/concepts/workloads/pods/pod-topology-spread-constraints/ |

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| Labyrinth Labs | <contact@lablabs.io> | <https://lablabs.io> |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
