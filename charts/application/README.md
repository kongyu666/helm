## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm repo add kongyu https://github.com/kongyu666/helm/tree/main/charts
$ helm install my-release kongyu/application 
```

These commands deploy application Open Source on the Kubernetes cluster in the default configuration.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Parameters

### Global parameters

| Name                      | Description                                     | Value |
| ------------------------- | ----------------------------------------------- | ----- |
| `global.imageRegistry`    | Global Docker image registry                    | `""`  |
| `global.storageClass`      | Global StorageClass for Persistent Volume(s)                                                                           | `""`  |
| `global.imagePullSecrets` | Global Docker registry secret names as an array | `[]`  |


### Common parameters

| Name                     | Description                                                  | Value           |
| ------------------------ | ------------------------------------------------------------ | --------------- |
| `nameOverride`           | String to partially override common.names.fullname template (will maintain the release name) | `""`            |
| `fullnameOverride`       | String to fully override common.names.fullname template      | `""`            |
| `namespaceOverride`      | String to fully override common.names.namespace              | `""`            |
| `kubeVersion`            | Force target Kubernetes version (using Helm capabilities if not set) | `""`            |
| `clusterDomain`          | Kubernetes Cluster Domain                                    | `cluster.local` |
| `extraDeploy`            | Extra objects to deploy (value evaluated as a template)      | `[]`            |
| `commonLabels`           | Add labels to all the deployed resources                     | `{}`            |
| `commonAnnotations`      | Add annotations to all the deployed resources                | `{}`            |
| `diagnosticMode.enabled` | Enable diagnostic mode (all probes will be disabled and the command will be overridden) | `false`         |
| `diagnosticMode.command` | Command to override all containers in the the deployment(s)/statefulset(s) | `["sleep"]`     |
| `diagnosticMode.args`    | Args to override all containers in the the deployment(s)/statefulset(s) | `["infinity"]`  |


### application parameters

| Name                 | Description                                                  | Value                              |
| -------------------- | ------------------------------------------------------------ | ---------------------------------- |
| `image.registry`     | application image registry                                   | `swr.cn-north-1.myhuaweicloud.com` |
| `image.repository`   | application image repository                                 | `kongyu/springboot-helloworld`     |
| `image.tag`          | application image tag (immutable tags are recommended)       | `v1.1`                             |
| `image.pullPolicy`   | application image pull policy                                | `IfNotPresent`                     |
| `image.pullSecrets`  | Specify docker-registry secret names as an array             | `[]`                               |
| `hostAliases`        | Deployment pod host aliases                                  | `[]`                               |
| `command`            | Override default container command (useful when using custom images) | `[]`                               |
| `args`               | Override default container args (useful when using custom images) | `[]`                               |
| `extraEnvVars`       | Extra environment variables to be set on application containers | `[]`                               |
| `extraEnvVarsCM`     | ConfigMap with extra environment variables                   | `""`                               |
| `extraEnvVarsSecret` | Secret with extra environment variables                      | `""`                               |


### application deployment parameters

| Name                                          | Description                                                  | Value                     |
| --------------------------------------------- | ------------------------------------------------------------ | ------------------------- |
| `replicaCount`                                | Number of application replicas to deploy                     | `1`                       |
| `updateStrategy.type`                         | application  deployment strategy type                        | `RollingUpdate`           |
| `updateStrategy.rollingUpdate`                | application deployment rolling update configuration parameters | `{}`                      |
| `podLabels`                                   | Additional labels for application pods                       | `{}`                      |
| `podAnnotations`                              | Annotations for application pods                             | `{}`                      |
| `podAffinityPreset`                           | Pod affinity preset. Ignored if `affinity` is set. Allowed values: `soft` or `hard` | `""`                      |
| `podAntiAffinityPreset`                       | Pod anti-affinity preset. Ignored if `affinity` is set. Allowed values: `soft` or `hard` | `soft`                    |
| `nodeAffinityPreset.type`                     | Node affinity preset type. Ignored if `affinity` is set. Allowed values: `soft` or `hard` | `""`                      |
| `nodeAffinityPreset.key`                      | Node label key to match Ignored if `affinity` is set.        | `""`                      |
| `nodeAffinityPreset.values`                   | Node label values to match. Ignored if `affinity` is set.    | `[]`                      |
| `affinity`                                    | Affinity for pod assignment                                  | `{}`                      |
| `hostNetwork`                                 | Specify if host network should be enabled for application pod | `false`                   |
| `hostIPC`                                     | Specify if host IPC should be enabled for application pod    | `false`                   |
| `nodeSelector`                                | Node labels for pod assignment. Evaluated as a template.     | `{}`                      |
| `tolerations`                                 | Tolerations for pod assignment. Evaluated as a template.     | `{}`                      |
| `priorityClassName`                           | application pods' priorityClassName                          | `""`                      |
| `schedulerName`                               | Name of the k8s scheduler (other than default)               | `""`                      |
| `terminationGracePeriodSeconds`               | In seconds, time the given to the application pod needs to terminate gracefully | `""`                      |
| `topologySpreadConstraints`                   | Topology Spread Constraints for pod assignment               | `[]`                      |
| `podSecurityContext.enabled`                  | Enabled application pods' Security Context                   | `false`                   |
| `podSecurityContext.fsGroup`                  | Set application pod's Security Context fsGroup               | `1001`                    |
| `podSecurityContext.sysctls`                  | sysctl settings of the application pods                      | `[]`                      |
| `containerSecurityContext.enabled`            | Enabled application containers' Security Context             | `false`                   |
| `containerSecurityContext.runAsUser`          | Set application container's Security Context runAsUser       | `1001`                    |
| `containerSecurityContext.runAsNonRoot`       | Set application container's Security Context runAsNonRoot    | `true`                    |
| `containerPorts.http`                         | Sets http port inside application container                  | `8080`                    |
| `containerPorts.https`                        | Sets https port inside application container                 | `""`                      |
| `configmap.enabled`                           | Create a configuration file                                  | `false`                   |
| `configmap.name`                              | The file name in the container                               | `"application.yaml"`      |
| `configmap.mountPath`                         | The mount path in the container                              | `"/opt/application.yaml"` |
| `configmap.configuration`                     | The contents of the file in the container                    | `""`                      |
| `resources.limits`                            | The resources limits for the application container           | `{}`                      |
| `resources.requests`                          | The requested resources for the application container        | `{}`                      |
| `lifecycleHooks`                              | Optional lifecycleHooks for the application container        | `{}`                      |
| `startupProbe.enabled`                        | Enable startupProbe                                          | `false`                   |
| `startupProbe.initialDelaySeconds`            | Initial delay seconds for startupProbe                       | `30`                      |
| `startupProbe.periodSeconds`                  | Period seconds for startupProbe                              | `10`                      |
| `startupProbe.timeoutSeconds`                 | Timeout seconds for startupProbe                             | `5`                       |
| `startupProbe.failureThreshold`               | Failure threshold for startupProbe                           | `6`                       |
| `startupProbe.successThreshold`               | Success threshold for startupProbe                           | `1`                       |
| `livenessProbe.enabled`                       | Enable livenessProbe                                         | `true`                    |
| `livenessProbe.initialDelaySeconds`           | Initial delay seconds for livenessProbe                      | `30`                      |
| `livenessProbe.periodSeconds`                 | Period seconds for livenessProbe                             | `10`                      |
| `livenessProbe.timeoutSeconds`                | Timeout seconds for livenessProbe                            | `5`                       |
| `livenessProbe.failureThreshold`              | Failure threshold for livenessProbe                          | `6`                       |
| `livenessProbe.successThreshold`              | Success threshold for livenessProbe                          | `1`                       |
| `readinessProbe.enabled`                      | Enable readinessProbe                                        | `true`                    |
| `readinessProbe.initialDelaySeconds`          | Initial delay seconds for readinessProbe                     | `5`                       |
| `readinessProbe.periodSeconds`                | Period seconds for readinessProbe                            | `5`                       |
| `readinessProbe.timeoutSeconds`               | Timeout seconds for readinessProbe                           | `3`                       |
| `readinessProbe.failureThreshold`             | Failure threshold for readinessProbe                         | `3`                       |
| `readinessProbe.successThreshold`             | Success threshold for readinessProbe                         | `1`                       |
| `customStartupProbe`                          | Custom liveness probe for the Web component                  | `{}`                      |
| `customLivenessProbe`                         | Override default liveness probe                              | `{}`                      |
| `customReadinessProbe`                        | Override default readiness probe                             | `{}`                      |
| `autoscaling.enabled`                         | Enable autoscaling for application deployment                | `false`                   |
| `autoscaling.minReplicas`                     | Minimum number of replicas to scale back                     | `""`                      |
| `autoscaling.maxReplicas`                     | Maximum number of replicas to scale out                      | `""`                      |
| `autoscaling.targetCPU`                       | Target CPU utilization percentage                            | `""`                      |
| `autoscaling.targetMemory`                    | Target Memory utilization percentage                         | `""`                      |
| `extraVolumes`                                | Array to add extra volumes                                   | `[]`                      |
| `extraVolumeMounts`                           | Array to add extra mount                                     | `[]`                      |
| `serviceAccount.create`                       | Enable creation of ServiceAccount for application pod        | `false`                   |
| `serviceAccount.name`                         | The name of the ServiceAccount to use.                       | `""`                      |
| `serviceAccount.annotations`                  | Annotations for service account. Evaluated as a template.    | `{}`                      |
| `serviceAccount.automountServiceAccountToken` | Auto-mount the service account token in the pod              | `false`                   |
| `sidecars`                                    | Sidecar parameters                                           | `[]`                      |
| `sidecarSingleProcessNamespace`               | Enable sharing the process namespace with sidecars           | `false`                   |
| `initContainers`                              | Extra init containers                                        | `[]`                      |
| `pdb.create`                                  | Created a PodDisruptionBudget                                | `false`                   |
| `pdb.minAvailable`                            | Min number of pods that must still be available after the eviction | `1`                       |
| `pdb.maxUnavailable`                          | Max number of pods that can be unavailable after the eviction | `0`                       |



### Traffic Exposure parameters

| Name                               | Description                                                  | Value                    |
| ---------------------------------- | ------------------------------------------------------------ | ------------------------ |
| `service.type`                     | Service type                                                 | `ClusterIP`              |
| `service.ports.http`               | Service HTTP port                                            | `80`                     |
| `service.ports.https`              | Service HTTPS port                                           | `""`                     |
| `service.nodePorts`                | Specify the nodePort(s) value(s) for the LoadBalancer and NodePort service types. | `{}`                     |
| `service.portNames`               | application service Port Name | `{}`                     |
| `service.targetPort`               | Target port reference value for the Loadbalancer service types can be specified explicitly. | `{}`                     |
| `service.clusterIP`                | application service Cluster IP                               | `""`                     |
| `service.loadBalancerIP`           | LoadBalancer service IP address                              | `""`                     |
| `service.loadBalancerSourceRanges` | application service Load Balancer sources                    | `[]`                     |
| `service.extraPorts`               | Extra ports to expose (normally used with the `sidecar` value) | `[]`                     |
| `service.sessionAffinity`          | Session Affinity for Kubernetes service, can be "None" or "ClientIP" | `None`                   |
| `service.sessionAffinityConfig`    | Additional settings for the sessionAffinity                  | `{}`                     |
| `service.annotations`              | Service annotations                                          | `{}`                     |
| `service.externalTrafficPolicy`    | Enable client source IP preservation                         | `Cluster`                |
| `ingress.enabled`                  | Set to true to enable ingress record generation              | `false`                  |
| `ingress.selfSigned`               | Create a TLS secret for this ingress record using self-signed certificates generated by Helm | `false`                  |
| `ingress.pathType`                 | Ingress path type                                            | `ImplementationSpecific` |
| `ingress.apiVersion`               | Force Ingress API version (automatically detected if not set) | `""`                     |
| `ingress.hostname`                 | Default host for the ingress resource                        | `application .local`     |
| `ingress.path`                     | The Path to application . You may need to set this to '/*' in order to use this with ALB ingress controllers. | `/`                      |
| `ingress.annotations`              | Additional annotations for the Ingress resource. To enable certificate autogeneration, place here your cert-manager annotations. | `{}`                     |
| `ingress.ingressClassName`         | Set the ingerssClassName on the ingress record for k8s 1.18+ | `""`                     |
| `ingress.tls`                      | Create TLS Secret                                            | `false`                  |
| `ingress.extraHosts`               | The list of additional hostnames to be covered with this ingress record. | `[]`                     |
| `ingress.extraPaths`               | Any additional arbitrary paths that may need to be added to the ingress under the main host. | `[]`                     |
| `ingress.extraTls`                 | The tls configuration for additional hostnames to be covered with this ingress record. | `[]`                     |
| `ingress.secrets`                  | If you're providing your own certificates, please use this to add the certificates as secrets | `[]`                     |
| `ingress.extraRules`               | The list of additional rules to be added to this ingress record. Evaluated as a template | `[]`                     |
| `healthIngress.enabled`            | Set to true to enable health ingress record generation       | `false`                  |
| `healthIngress.selfSigned`         | Create a TLS secret for this ingress record using self-signed certificates generated by Helm | `false`                  |
| `healthIngress.pathType`           | Ingress path type                                            | `ImplementationSpecific` |
| `healthIngress.hostname`           | When the health ingress is enabled, a host pointing to this will be created | `example.local`          |
| `healthIngress.path`               | Default path for the ingress record                          | `/`                      |
| `healthIngress.annotations`        | Additional annotations for the Ingress resource. To enable certificate autogeneration, place here your cert-manager annotations. | `{}`                     |
| `healthIngress.tls`                | Enable TLS configuration for the hostname defined at `healthIngress.hostname` parameter | `false`                  |
| `healthIngress.extraHosts`         | An array with additional hostname(s) to be covered with the ingress record | `[]`                     |
| `healthIngress.extraPaths`         | An array with additional arbitrary paths that may need to be added to the ingress under the main host | `[]`                     |
| `healthIngress.extraTls`           | TLS configuration for additional hostnames to be covered     | `[]`                     |
| `healthIngress.secrets`            | TLS Secret configuration                                     | `[]`                     |
| `healthIngress.ingressClassName`   | IngressClass that will be be used to implement the Ingress (Kubernetes 1.18+) | `""`                     |
| `healthIngress.extraRules`         | The list of additional rules to be added to this ingress record. Evaluated as a template | `[]`                     |

### Persistence parameters

| Name                         | Description                                                  | Value               |
| ---------------------------- | ------------------------------------------------------------ | ------------------- |
| `persistence.enabled`        | Enable application data persistence using PVC                | `true`              |
| `persistence.existingClaim`  | Provide an existing `PersistentVolumeClaim` (only when `architecture=standalone`) | `""`                |
| `persistence.resourcePolicy` | Setting it to "keep" to avoid removing PVCs during a helm delete operation. Leaving it empty will delete PVCs after the chart deleted | `""`                |
| `persistence.storageClass`   | PVC Storage Class for application data volume                | `""`                |
| `persistence.accessModes`    | PV Access Mode                                               | `["ReadWriteOnce"]` |
| `persistence.size`           | PVC Storage Request for application data volume              | `10Gi`              |
| `persistence.annotations`    | PVC annotations                                              | `{}`                |
| `persistence.mountPath`      | Path to mount the volume at                                  | `/opt/logs`         |


Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
$ helm install my-release \
  --set imagePullPolicy=Always \
    kongyu/application 
```

The above command sets the `imagePullPolicy` to `Always`.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install my-release -f values.yaml kongyu/application 
```

> **Tip**: You can use the default [values.yaml](values.yaml)

