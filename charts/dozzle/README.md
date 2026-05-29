# Dozzle Helm Chart

This chart deploys Dozzle in Kubernetes mode using the RBAC, Deployment, and Service resources from `examples/k8s.dozzle.yml` as the baseline.

## Install locally

```bash
helm install dozzle ./charts/dozzle --namespace dozzle --create-namespace
```

## Render manifests

```bash
helm template dozzle ./charts/dozzle
```

## Publish as a Helm repository

Package the chart and generate an index for a static Helm repository:

```bash
helm package charts/dozzle --destination .helm-repo
helm repo index .helm-repo --url https://example.com/helm
```

Publish the contents of `.helm-repo` to the static URL, then use it with Helm 3:

```bash
helm repo add dozzle https://example.com/helm
helm install dozzle dozzle/dozzle --namespace dozzle --create-namespace
```

## Common values

```yaml
image:
  repository: amir20/dozzle
  tag: latest

env:
  DOZZLE_MODE: k8s
  DOZZLE_LEVEL: debug

ingress:
  enabled: true
  hosts:
    - host: dozzle.example.com
      paths:
        - path: /
          pathType: Prefix
```
