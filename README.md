# k8s-target-allocator

This is the companion repo to [this video (coming soon)](https://example.com).

In the video I use [Headlamp](https://headlamp.dev). It's a great local cluster viewer from the CNCF.

## Basic

Download OpenObserve from [here](https://github.com/openobserve/openobserve/releases)

```
kind create cluster
helm repo add jetstack https://charts.jetstack.io --force-update
helm upgrade -i \
  cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --create-namespace \
  --version v1.18.2 \
  --set crds.enabled=true \
  --set prometheus.enabled=true

kubectl apply -f https://github.com/open-telemetry/opentelemetry-operator/releases/latest/download/opentelemetry-operator.yaml

echo -n "Basic YOUR_VALUE_HERE" | base64

kubectl apply -f otelcol-basic.yaml
```

## Advanced

1. Stop OpenObserve
2. Delete the `data/openobserve` folders to ensure you start from zero.
3. Restart OpenObserve

```
kind create cluster
kubectl apply -f https://raw.githubusercontent.com/prometheus-community/helm-charts/refs/heads/main/charts/kube-prometheus-stack/charts/crds/crds/crd-servicemonitors.yaml
helm upgrade -i \
  cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --create-namespace \
  --version v1.18.2 \
  --set crds.enabled=true \
  --set prometheus.enabled=true \
  --set prometheus.servicemonitor.enabled=true

echo -n "Basic YOUR_VALUE_HERE" | base64

kubectl apply -f https://github.com/open-telemetry/opentelemetry-operator/releases/latest/download/opentelemetry-operator.yaml

kubectl apply -f otelcol-advanced.yaml
```
