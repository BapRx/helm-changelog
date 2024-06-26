# Change Log

## 0.3.0

**Release date:** 2023-05-30

![AppVersion: v0.6.0](https://img.shields.io/static/v1?label=AppVersion&message=v0.6.0&color=success)
![Helm: v3](https://img.shields.io/static/v1?label=Helm&message=v3&color=informational&logo=helm)

* [prom-label-proxy] add ServiceMonitor suuport (#3249)

### Default value changes

```diff
diff --git a/charts/prom-label-proxy/values.yaml b/charts/prom-label-proxy/values.yaml
index 560c2a23..ccd87601 100644
--- a/charts/prom-label-proxy/values.yaml
+++ b/charts/prom-label-proxy/values.yaml
@@ -120,3 +120,76 @@ config:
   extraArgs:
     - "--enable-label-apis=true"
     - "--error-on-replace=true"
+
+# Metrics setttings.
+metrics:
+  # If enabled, supply metrics.
+  enabled: false
+
+  # Listen address for metrics.
+  listenAddress: 0.0.0.0:9090
+
+  # ServiceMonitor setttings.
+  serviceMonitor:
+
+    # If enabled, create ServiceMonitor.
+    enabled: false
+
+    # Service port for metrics.
+    port: 9090
+
+    # Additional labels for ServiceMonitor.
+    additionalLabels: {}
+
+    # JobLabel selects the label from the associated Kubernetes service which will be used as the job label for all metrics.
+    jobLabel: ""
+
+    # TargetLabels transfers labels from the Kubernetes Service onto the created metrics.
+    targetLabels: []
+
+    # PodTargetLabels transfers labels on the Kubernetes Pod onto the created metrics.
+    podTargetLabels: []
+
+    # SampleLimit defines per-scrape limit on number of scraped samples that will be accepted.
+    sampleLimit: 0
+
+    # TargetLimit defines a limit on the number of scraped targets that will be accepted.
+    targetLimit: 0
+
+    # Per-scrape limit on number of labels that will be accepted for a sample. Only valid in Prometheus versions 2.27.0 and newer.
+    labelLimit: 0
+
+    # Per-scrape limit on length of labels name that will be accepted for a sample. Only valid in Prometheus versions 2.27.0 and newer.
+    labelNameLengthLimit: 0
+
+    # Per-scrape limit on length of labels value that will be accepted for a sample. Only valid in Prometheus versions 2.27.0 and newer.
+    labelValueLengthLimit: 0
+
+    # Attaches node metadata to discovered targets. Requires Prometheus v2.37.0 and above.
+    attachMetadata: {}
+
+    # Additional settings for ServiceMonitor.
+    additionalConfigs: {}
+
+    # HonorLabels chooses the metric’s labels on collisions with target labels.
+    honorLabels: false
+
+    # HonorTimestamps controls whether Prometheus respects the timestamps present in scraped data.
+    honorTimestamps: null
+
+    # Interval at which metrics should be scraped.
+    interval: ""
+
+    # Timeout after which the scrape is ended.
+    scrapeTimeout: ""
+
+    # RelabelConfigs to apply to samples before scraping
+    # ref: https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#relabelconfig
+    relabelings: []
+
+    # MetricRelabelConfigs to apply to samples after scraping, but before ingestion.
+    # ref: https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#relabelconfig
+    metricRelabelings: []
+
+    # Additional settings for Endpoint.
+    additionalEndpointConfigs: {}

```

## 0.2.0

**Release date:** 2023-02-08

![AppVersion: v0.6.0](https://img.shields.io/static/v1?label=AppVersion&message=v0.6.0&color=success)
![Helm: v3](https://img.shields.io/static/v1?label=Helm&message=v3&color=informational&logo=helm)

* Add podLabels to prom-label-proxy (#3000)

### Default value changes

```diff
diff --git a/charts/prom-label-proxy/values.yaml b/charts/prom-label-proxy/values.yaml
index 205a9f7c..560c2a23 100644
--- a/charts/prom-label-proxy/values.yaml
+++ b/charts/prom-label-proxy/values.yaml
@@ -33,6 +33,9 @@ serviceAccount:
 # -- Annotations for prom-label-proxy pods
 podAnnotations: {}
 
+# -- Labels for prom-label-proxy pods
+podLabels: {}
+
 # -- prom-label-proxy pods' Security Context.
 podSecurityContext: {}
   # fsGroup: 2000

```

## 0.1.0

**Release date:** 2022-07-13

![AppVersion: v0.5.0](https://img.shields.io/static/v1?label=AppVersion&message=v0.5.0&color=success)
![Helm: v3](https://img.shields.io/static/v1?label=Helm&message=v3&color=informational&logo=helm)

* [prom-label-proxy] Setup chart (#2269)
* Revert "feat: prom-label-proxy (#2262)" (#2267)

### Default value changes

```diff
# No changes in this release
```

## 1.0.0

**Release date:** 2022-07-12

![AppVersion: v0.5.0](https://img.shields.io/static/v1?label=AppVersion&message=v0.5.0&color=success)
![Helm: v3](https://img.shields.io/static/v1?label=Helm&message=v3&color=informational&logo=helm)

* feat: prom-label-proxy (#2262)

### Default value changes

```diff
# -- Number of prom-label-proxy replicas to deploy
replicaCount: 1

image:
  pullPolicy: IfNotPresent
  # -- prom-label-proxy image registry
  repository: quay.io/prometheuscommunity/prom-label-proxy
  # -- prom-label-proxy image tag (immutable tags are recommended).
  # @default -- `.Chart.AppVersion`
  tag: ""

# -- registry secret names as an array
imagePullSecrets: []

# -- String to partially override prom-label-proxy.fullname template (will maintain the release name)
nameOverride: ""

# -- Override the namespace
namespaceOverride: ""

# -- String to fully override amazon-eks-pod-identity.fullname template
fullnameOverride: ""

serviceAccount:
  # -- Enable creation of ServiceAccount for nginx pod
  create: true
  # -- The name of the ServiceAccount to use.
  # @default -- A name is generated using the `prom-label-proxy.fullname` template
  name: ''
  # -- Annotations for service account. Evaluated as a template.
  annotations: {}

# -- Annotations for prom-label-proxy pods
podAnnotations: {}

# -- prom-label-proxy pods' Security Context.
podSecurityContext: {}
  # fsGroup: 2000

securityContext:
  runAsUser: 65534
  runAsGroup: 65534
  runAsNonRoot: true
  readOnlyRootFilesystem: true

service:
  port: 8080
  # -- Service type
  type: ClusterIP
  # -- Service annotations
  annotations: {}

livenessProbe:
  httpGet:
    # -- This is the liveness check endpoint
    path: /healthz
    port: http

readinessProbe:
  httpGet:
    # -- This is the readiness check endpoint
    path: /healthz
    port: http

resources:
  # -- The resources limits for the prom-label-proxy container
  ## Example:
  ## limits:
  ##    cpu: 100m
  ##    memory: 128Mi
  limits:
    cpu: 200m
    memory: 128Mi
  # -- The requested resources for the prom-label-proxy container
  ## Examples:
  ## requests:
  ##    cpu: 100m
  ##    memory: 128Mi
  requests:
    cpu: 100m
    memory: 64Mi

# -- Affinity for pod assignment
affinity: {}

# -- Node labels for pod assignment. Evaluated as a template.
nodeSelector: {}

# -- Tolerations for pod assignment. Evaluated as a template.
tolerations: []

ingress:
  enabled: false
  className: ""
  labels: {}
  annotations: {}
    # kubernetes.io/ingress.class: nginx
    # kubernetes.io/tls-acme: "true"
  hosts:
    - host: chart-example.local
      paths:
        - path: /
          pathType: ImplementationSpecific
  tls: []
  #  - secretName: chart-example-tls
  #    hosts:
  #      - chart-example.local

config:
  # -- listen address
  listenAddress: 0.0.0.0:8080
  # -- The upstream URL to proxy to
  upstream: "http://prometheus:9090"
  # -- The label to enforce in all proxies PromQL queries.
  label: "namespace"
  # -- Additional arguments for prom-label-proxy
  extraArgs:
    - "--enable-label-apis=true"
    - "--error-on-replace=true"

```

---
Autogenerated from Helm Chart and git history using [helm-changelog](https://github.com/mogensen/helm-changelog)
