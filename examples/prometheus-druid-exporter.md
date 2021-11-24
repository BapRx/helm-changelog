# Change Log

## 0.9.0 

**Release date:** 2020-11-22

![AppVersion: v0.8.0](https://img.shields.io/static/v1?label=AppVersion&message=v0.8.0&color=success&logo=)
![Helm: v2](https://img.shields.io/static/v1?label=Helm&message=v2&color=inactive&logo=helm)
![Helm: v3](https://img.shields.io/static/v1?label=Helm&message=v3&color=informational&logo=helm)


* [prometheus-druid-exporter] support podAnnotations (#306) 

### Default value changes

```diff
diff --git a/charts/prometheus-druid-exporter/values.yaml b/charts/prometheus-druid-exporter/values.yaml
index 2d70aca..486098a 100644
--- a/charts/prometheus-druid-exporter/values.yaml
+++ b/charts/prometheus-druid-exporter/values.yaml
@@ -8,6 +8,8 @@ image:
 
 annotations: {}
 
+podAnnotations: {}
+
 druidURL: http://druid.opstreelabs.in
 logLevel: info
 logFormat: json
```

## 0.8.1 

**Release date:** 2020-10-24

![AppVersion: v0.8.0](https://img.shields.io/static/v1?label=AppVersion&message=v0.8.0&color=success&logo=)
![Helm: v2](https://img.shields.io/static/v1?label=Helm&message=v2&color=inactive&logo=helm)
![Helm: v3](https://img.shields.io/static/v1?label=Helm&message=v3&color=informational&logo=helm)


* if not enable serviceMonitor, it will auto add annotations to yaml (#254) 

### Default value changes

```diff
# No changes in this release
```

## 0.8.0 

**Release date:** 2020-10-12

![AppVersion: v0.8.0](https://img.shields.io/static/v1?label=AppVersion&message=v0.8.0&color=success&logo=)
![Helm: v2](https://img.shields.io/static/v1?label=Helm&message=v2&color=inactive&logo=helm)
![Helm: v3](https://img.shields.io/static/v1?label=Helm&message=v3&color=informational&logo=helm)


* [prometheus-druid-exporter] Added druid exporter (#114) 

### Default value changes

```diff
---
name: druid-exporter

image:
  name: quay.io/opstree/druid-exporter
  tag: v0.8
  pullPolicy: IfNotPresent

annotations: {}

druidURL: http://druid.opstreelabs.in
logLevel: info
logFormat: json

exporterPort: 8080

serviceAccount:
  create: true

serviceType: ClusterIP

serviceMonitor:
  enabled: false
  namespace: monitoring
  interval: 30s
  scrapeTimeout: 10s
  additionalLabels: {}
  targetLabels: []
```

---
Autogenerated from Helm Chart and git history using [helm-changelog](https://github.com/mogensen/helm-changelog)