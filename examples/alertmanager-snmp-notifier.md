# Change Log

## 0.1.1

**Release date:** 2023-05-26

![AppVersion: v1.4.0](https://img.shields.io/static/v1?label=AppVersion&message=v1.4.0&color=success)
![Helm: v3](https://img.shields.io/static/v1?label=Helm&message=v3&color=informational&logo=helm)

* [alertmanager-snmp-notifier] Values json schema (#3407)

### Default value changes

```diff
diff --git a/charts/alertmanager-snmp-notifier/values.yaml b/charts/alertmanager-snmp-notifier/values.yaml
index bfa6dad7..aefdd090 100644
--- a/charts/alertmanager-snmp-notifier/values.yaml
+++ b/charts/alertmanager-snmp-notifier/values.yaml
@@ -146,7 +146,7 @@ serviceMonitor:
   # Set path to cloudwatch-exporter telemtery-path
   telemetryPath: /metrics
   # Set labels for the ServiceMonitor, use this to define your scrape label for Prometheus Operator
-  labels:
+  labels: {}
   # Set timeout for scrape
   timeout: 10s
   # Set of labels to transfer from the Kubernetes Service onto the target

```

## 0.1.0

**Release date:** 2023-02-01

![AppVersion: v1.4.0](https://img.shields.io/static/v1?label=AppVersion&message=v1.4.0&color=success)
![Helm: v3](https://img.shields.io/static/v1?label=Helm&message=v3&color=informational&logo=helm)

* [alertmanager-snmp-notifier] add SNMP notifer chart (#2898)

### Default value changes

```diff
image:
  repository: maxwo/snmp-notifier
  pullPolicy: IfNotPresent
  # Overrides the image tag whose default is the chart appVersion.
  tag: ""

imagePullSecrets: []
nameOverride: ""
fullnameOverride: ""

snmpNotifier:
  # extraArgs allows to pass SNMP notifier configurations, as described on https://github.com/maxwo/snmp_notifier#snmp-notifier-configuration
  extraArgs: []
  # - --alert.severity-label=severity

  # snmpDestinations is the list of SNMP servers to send the traps to
  snmpDestinations:
    - snmp-server:162

  # SNMP authentication secrets, that may be instanciated by the chart, or may use an already created secret
  # snmpCommunity: public
  # snmpAuthenticationUsername: my_authentication_username
  # snmpAuthenticationPassword: my_authentication_password
  # snmpPrivatePassword: my_private_password
  # snmpCommunitySecret:
  #   name: existingsecret
  #   key: community
  # snmpAuthenticationUsernameSecret:
  #   name: existingsecret
  #   key: authenticationUsername
  # snmpAuthenticationPasswordSecret:
  #   name: existingsecret
  #   key: authenticationPassword
  # snmpPrivatePasswordSecret:
  #   name: existingsecret
  #   key: privatePassword

  # snmpTemplates allows to customize the description of the traps, and add extra trap fields
  snmpTemplates: {}
  #   description: |
  #     {{- if .Alerts -}}
  #     {{ len .Alerts }}/{{ len .DeclaredAlerts }} alerts are firing:

  #     {{ range $severity, $alerts := (groupAlertsByLabel .Alerts "severity") -}}
  #     Status: {{ $severity }}

  #     {{- range $index, $alert := $alerts }}
  #     - Alert: {{ $alert.Labels.alertname }}
  #       Summary: {{ $alert.Annotations.summary }}
  #       Description: {{ $alert.Annotations.description }}
  #     {{ end }}
  #     {{ end }}
  #     {{ else -}}
  #     Status: OK
  #     {{- end -}}

  #   extraFields:
  #     - subId: 4
  #       template: |
  #         {{- if .Alerts -}}
  #         Status: NOK
  #         {{- else -}}
  #         Status: OK
  #         {{- end -}}
  #     - subId: 5
  #       template: |
  #         This is a constant

serviceAccount:
  # Specifies whether a service account should be created
  create: true
  # Annotations to add to the service account
  annotations: {}
  # The name of the service account to use.
  # If not set and create is true, a name is generated using the fullname template
  name: ""

podAnnotations: {}

podSecurityContext: {}
  # fsGroup: 2000

replicaCount: 1

securityContext: {}
  # capabilities:
  #   drop:
  #   - ALL
  # readOnlyRootFilesystem: true
  # runAsNonRoot: true
  # runAsUser: 1000

service:
  type: ClusterIP
  port: 9464

ingress:
  enabled: false
  className: ""
  annotations: {}
    # kubernetes.io/ingress.class: nginx
    # kubernetes.io/tls-acme: "true"
  hosts:
    - host: snmp-notifier.local
      paths:
        - path: /
          pathType: ImplementationSpecific
  tls: []
  #  - secretName: snmp-notifier-tls
  #    hosts:
  #      - snmp-notifier.local

resources: {}
  # We usually recommend not to specify default resources and to leave this as a conscious
  # choice for the user. This also increases chances charts run on environments with little
  # resources, such as Minikube. If you do want to specify resources, uncomment the following
  # lines, adjust them as necessary, and remove the curly braces after 'resources:'.
  # limits:
  #   cpu: 100m
  #   memory: 128Mi
  # requests:
  #   cpu: 100m
  #   memory: 128Mi

autoscaling:
  enabled: false
  minReplicas: 1
  maxReplicas: 100
  targetCPUUtilizationPercentage: 80
  # targetMemoryUtilizationPercentage: 80

nodeSelector: {}

tolerations: []

affinity: {}

# Enable this if you're using https://github.com/coreos/prometheus-operator
serviceMonitor:
  # When set true then use a ServiceMonitor to configure scraping
  enabled: false
  # Set the namespace the ServiceMonitor should be deployed
  namespace: monitoring
  # Set how frequently Prometheus should scrape
  interval: 30s
  # Set path to cloudwatch-exporter telemtery-path
  telemetryPath: /metrics
  # Set labels for the ServiceMonitor, use this to define your scrape label for Prometheus Operator
  labels:
  # Set timeout for scrape
  timeout: 10s
  # Set of labels to transfer from the Kubernetes Service onto the target
  targetLabels: []
  # MetricRelabelConfigs to apply to samples before ingestion
  metricRelabelings: []
  # Set relabel_configs as per https://prometheus.io/docs/prometheus/latest/configuration/configuration/#relabel_config
  relabelings: []

```

---
Autogenerated from Helm Chart and git history using [helm-changelog](https://github.com/mogensen/helm-changelog)
