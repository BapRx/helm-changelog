# Change Log

## 0.4.0

**Release date:** 2023-05-23

![AppVersion: 0.65.1](https://img.shields.io/static/v1?label=AppVersion&message=0.65.1&color=success)
![Helm: v3](https://img.shields.io/static/v1?label=Helm&message=v3&color=informational&logo=helm)

* [prometheus-operator-admission-webhook] Bump app version to 0.65.1 (#3404)

### Default value changes

```diff
# No changes in this release
```

## 0.3.1

**Release date:** 2023-05-02

![AppVersion: 0.64.1](https://img.shields.io/static/v1?label=AppVersion&message=0.64.1&color=success)
![Helm: v3](https://img.shields.io/static/v1?label=Helm&message=v3&color=informational&logo=helm)

* [prometheus-operator-admission-webhook] Bump appVersion to 0.64.1 (#3285)

### Default value changes

```diff
# No changes in this release
```

## 0.3.0

**Release date:** 2023-04-21

![AppVersion: 0.64.0](https://img.shields.io/static/v1?label=AppVersion&message=0.64.0&color=success)
![Helm: v3](https://img.shields.io/static/v1?label=Helm&message=v3&color=informational&logo=helm)

* [prometheus-operator-admission-webhook] Apply corrections (#3269)

### Default value changes

```diff
diff --git a/charts/prometheus-operator-admission-webhook/values.yaml b/charts/prometheus-operator-admission-webhook/values.yaml
index dee1b9a7..c2780dcc 100644
--- a/charts/prometheus-operator-admission-webhook/values.yaml
+++ b/charts/prometheus-operator-admission-webhook/values.yaml
@@ -349,5 +349,3 @@ networkPolicy:
   ## Additional labels and annotations to attach to network policy
   labels: {}
   annotations: {}
-  ## If true, limit access only from namespace labelled name=monitoring
-  allowMonitoringNamespace: false

```

## 0.2.1

**Release date:** 2023-04-19

![AppVersion: 0.64.0](https://img.shields.io/static/v1?label=AppVersion&message=0.64.0&color=success)
![Helm: v3](https://img.shields.io/static/v1?label=Helm&message=v3&color=informational&logo=helm)

* [prometheus-operator-admission-webhook] Correct webhook configurations (#3262)

### Default value changes

```diff
# No changes in this release
```

## 0.2.0

**Release date:** 2023-04-15

![AppVersion: 0.64.0](https://img.shields.io/static/v1?label=AppVersion&message=0.64.0&color=success)
![Helm: v3](https://img.shields.io/static/v1?label=Helm&message=v3&color=informational&logo=helm)

* Bump appVersion to 0.64.0 (#3229)

### Default value changes

```diff
# No changes in this release
```

## 0.1.0

**Release date:** 2023-04-12

![AppVersion: 0.63.0](https://img.shields.io/static/v1?label=AppVersion&message=0.63.0&color=success)
![Helm: v3](https://img.shields.io/static/v1?label=Helm&message=v3&color=informational&logo=helm)

* [prometheus-operator-admission-webhook] Add chart prometheus-operator… (#3208)

### Default value changes

```diff
## Default values for prometheus-operator-admission-webhook
## This is a YAML-formatted file.
## Declare variables to be passed into your templates.

## namespaceOverride overrides the namespace which the resources will be deployed in
namespaceOverride: ""

## fullnameOverride overrides "release name"-"chart name" with a custom string
fullnameOverride: ""

## nameOverride overrides "chart name" with a custom string
nameOverride: ""

## kubeVersionOverride overrides Kubernetes version
kubeVersionOverride: ""

## webhooks provides parameters for webhook configurations.
## failurePolicy: Fail or Ignore, default Fail
## timeoutSeconds: 1 to 30, default 10
## namespaceSelector: {}, defaults to all objects irrespective of their namespace
## For info on converting Alertmanagerconfigs,
## see https://prometheus-operator.dev/docs/user-guides/webhook/#converting-alertmanagerconfig-resources
webhooks:
  failurePolicy: Fail
  timeoutSeconds: 10
  namespaceSelector: {}

  ## Additional labels and annotations for webhook configurations
  labels: {}
  annotations: {}

## jobs enables creation of a TLS keypair and a patch of webhook configurations.
## Jobs and related resources are hooks. Their output is a TLS key pair
## with a CA certificate stored in a secret and update of the
## caBundle field in webhook configurations. Should not be used
## whilst cert-manager or tlsSecret is enabled.
jobs:
  enabled: true

  ## Additional labels and annotations
  annotations: {}
  labels: {}

  ## securityContext for pod
  securityContext: {}

  ## containerSecurityContext sets security context for containers
  containerSecurityContext:
    allowPrivilegeEscalation: false
    capabilities:
      drop: ["ALL"]
    readOnlyRootFilesystem: true
    runAsGroup: 10000
    runAsNonRoot: true
    runAsUser: 10000
    seccompProfile:
      type: RuntimeDefault

  ## image sets image-related parameters for jobs' containers
  image:
    registry: registry.k8s.io
    repository: ingress-nginx/kube-webhook-certgen
    tag: "v20221220-controller-v1.5.1-58-g787ea74b6"
    ## sha256 digest overrides tag
    # digest: 4d99688e557396f5baa150e019ff7d5b7334f9b9f9a8dab64038c5c2a006f6b5
    digest: ""
    pullPolicy: Always
    pullSecrets: []

  ## priorityClassName for pods
  priorityClassName: ""

  ## resources for job containers
  ## Ref. https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/
  ## We usually recommend not to specify default resources and to leave this as a conscious
  ## choice for the user. This also increases chances charts run on environments with little
  ## resources, such as Minikube. If you do want to specify resources, uncomment the following
  ## lines, adjust them as necessary, and remove the curly braces after 'resources:'.
  resources: {}
    # limits:
    #   cpu: 100m
    #   memory: 64Mi
    # requests:
    #   cpu: 50m
    #   memory: 64Mi

  ## affinity
  affinity: {}

  ## nodeSelector
  nodeSelector: {}

  ## tolerations
  tolerations: {}

## certManager enables cert-manager to generate certificate for the webhook.
## caBundle and jobs should not be set.
certManager:
  enabled: false
  ## issuerRef references an existing issuer for the webhook certificate.
  ## An issuer represents a certificate issuing authority.
  ## If not set, new issuers will be created.
  ## ref. https://cert-manager.io/docs/reference/api-docs/#cert-manager.io/v1.Issuer
  issuerRef: ""
  ## rootCert allows setting certificate's lifetime when creating an issuer, defaults to 5y
  rootCert: {}
    # duration: "43800h0m0s"
  ## webhookCert allows setting webhook certificate's lifetime, defaults to 1y
  webhookCert: {}
    # duration: "8760h0m0s"

## caBundle allows inserting a CA bundle in webhook configurations
## (PEM format, base64-encoded) if that CA is unknown at the API server.
## The same CA signed the webhook's certificate set in tlsSecret.
## certManager and jobs should not be enabled.
## Can remain unset if the CA is known as trusted at the API server.
caBundle: ""

## tlsSecret references a secret holding the corresponding
## TLS key under key keyItem and certificate under key certItem
## to be used by the webhook.
## Default items assumed in the secret are
## tls.crt and tls.key for certificate and key, respectively.
tlsSecret: {}
  # name: prometheus-operator-admission-webhook-tls
  # keyItem: ""
  # certItem: ""

## tlsMinVersion is the minimum TLS version the webhook supports
tlsMinVersion: "VersionTLS13"

## extraArgs for additional arguments passed to the container command
extraArgs: []
  # - --log-level=debug
  # - --log-format=json

## containerPort sets port of the webhook container
containerPort: 10250

## replicas sets a number of pods to start. For high availability
## of the webhook, set at least 2.
replicas: 1

## restartPolicy
restartPolicy: Always

## podDisruptionBudget sets min/max number of available/unavailable replicas at a time
podDisruptionBudget: {}
  # maxUnavailable: 0

## affinity
affinity: {}

## automountServiceAccountToken allows mounting the service account token automatically
## for other containers to consume
automountServiceAccountToken: false

## env sets environment variables to pass to the container. Can be set as name/value pairs,
## read from secrets or configmaps.
env: []
  # - name: VAR1
  #   value: value1
  # - name: PASSWORD
  #   valueFrom:
  #     secretKeyRef:
  #       name: mysecret
  #       key: password
  #       optional: false

## initContainers specifies init containers to execute in the pod
## Ref. https://kubernetes.io/docs/concepts/workloads/pods/init-containers/
initContainers: []

## extraContainers specifies additional containers to start in the pod
extraContainers: []

## updateStrategy sets a way of how the deployment gets updated
updateStrategy:
  type: RollingUpdate
  rollingUpdate:
    maxSurge: 1
    maxUnavailable: 0

## rbac allows creating roles and pod security policy
## Ref. https://kubernetes.io/docs/concepts/security/pod-security-policy/
rbac:
  create: true
  pspEnabled: false

## image sets webhook container image parameters
image:
  registry: quay.io
  repository: prometheus-operator/admission-webhook
  ## Tag follows Chart.AppVersion by default
  tag: ""
  ## sha256 digest overrides tag
  # digest: 3cd905af5c5504a93e6095af1cfd1db05cd4e1c3fc4ac488fc37fa71b057c93d
  digest: ""
  pullPolicy: Always
  pullSecrets: []
    # - registrySecret

## serviceAccount for service account configuration
serviceAccount:
  create: true
  name: ""
  annotations: {}
  labels: {}

## securityContext for pod
## Ref. https://kubernetes.io/docs/tasks/configure-pod-container/security-context/
securityContext:
  fsGroup: 2000

## containerSecurityContext sets security context for container
containerSecurityContext:
  allowPrivilegeEscalation: false
  capabilities:
    drop: ["ALL"]
  readOnlyRootFilesystem: true
  runAsGroup: 1000
  runAsNonRoot: true
  runAsUser: 1000
  seccompProfile:
    type: RuntimeDefault

## livenessProbe sets liveness probe parameters
## Ref. https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/
livenessProbe:
  tcpSocket:
    port: https
  periodSeconds: 10
  initialDelaySeconds: 5

## readinessProbe sets readiness probe parameters
readinessProbe:
  httpGet:
    path: /healthz
    port: https
    scheme: HTTPS
  periodSeconds: 10

## nodeSelector
nodeSelector: {}

## resources for the webhook container
## Ref. https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/
## We usually recommend not to specify default resources and to leave this as a conscious
## choice for the user. This also increases chances charts run on environments with little
## resources, such as Minikube. If you do want to specify resources, uncomment the following
## lines, adjust them as necessary, and remove the curly braces after 'resources:'.
resources: {}
  # limits:
  #   cpu: 100m
  #   memory: 200Mi
  # requests:
  #   cpu: 100m
  #   memory: 200Mi

## deployment allows setting additional labels and annotations for deployment
deployment:
  annotations: {}
  labels: {}

## pod allows setting additional labels and annotations for pod
pod:
  annotations: {}
  labels: {}

## priorityClass for the pod
priorityClassName: ""

## service sets configuration for the webhook service. Service type ClusterIP is supported
## and set by default.
service:
  annotations: {}
  labels: {}
  port: 443

## tolerations
tolerations: []

## prometheusRule for creating prometheus rules
## https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#monitoring.coreos.com/v1.PrometheusRule
prometheusRule:
  enabled: false
  ## Override namespace where the rules get deployed
  namespace: ""
  annotations: {}
  ## Add labels to match rule selectors
  labels: {}
    # release: kube-prometheus-stack
  rules: []
    # - alert: Admission webhook target down
    #   expr: up{namespace="{{ include "prometheus-operator-admission-webhook.namespace" . }}",
    #       service="{{ include "prometheus-operator-admission-webhook.fullname" . }}"} == 0
    #   for: 5m
    #   labels:
    #     severity: warning
    #   annotations:
    #     summary: Scraping {{`{{ $labels.pod }}`}}/{{`{{ $labels.container }}`}}
    #       in namespace {{`{{ $labels.namespace }}`}} failed.

## serviceMonitor allows creating a service monitor for Prometheus operator to assemble corresponding
## configuration for Prometheus
## Ref. https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#monitoring.coreos.com/v1.ServiceMonitor
serviceMonitor:
  ## Enable service monitor
  enabled: false
  ## Overrides namespace where the service monitor gets deployed
  namespace: ""
  ## Override default job label
  jobLabel: ""
  ## MetricRelabelConfigs to apply to samples before ingestion
  metricRelabeling: []
  ## RelabelConfigs to apply to targets before scraping
  relabelings: []
  ## Add labels to match service monitor selectors
  labels: {}
    # release: kube-prometheus-stack
  ## TargetLabels transfers labels from the Kubernetes Service onto the created metrics
  targetLabels: []
  ## Add annotations to the service monitor
  annotations: {}
  ## Scrape interval
  interval: 30s
  ## Scrape timeout
  scrapeTimeout: 10s
  ## HonorLabels chooses the metric labels on collisions with target labels
  honorLabels: false
  ## Attach node metadata to discovered targets. Requires Prometheus v2.37.0 and above.
  attachMetadata:
    node: false
  ## TLS configuration to use at scraping the endpoint. The webhook always supports TLS,
  ## so that tlsConfig is required. The given secret must exist in the service monitor's namespace.
  tlsConfig: {}
    # serverName: "prometheus-operator-admission-webhook.monitoring.svc"
    # ca:
    #   secret:
    #     name: "prometheus-operator-admission-webhook-ca"
    #     key: ca
    # insecureSkipVerify: false

## networkPolicy allows enabling network policy with custom restrictions
## Ref. https://kubernetes.io/docs/concepts/services-networking/network-policies/
networkPolicy:
  ## Enable network policy and allows access from anywhere
  enabled: false
  ## Additional labels and annotations to attach to network policy
  labels: {}
  annotations: {}
  ## If true, limit access only from namespace labelled name=monitoring
  allowMonitoringNamespace: false

```

---
Autogenerated from Helm Chart and git history using [helm-changelog](https://github.com/mogensen/helm-changelog)
