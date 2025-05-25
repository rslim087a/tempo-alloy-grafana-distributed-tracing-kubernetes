# 1. Create namespace
```
kubectl create namespace monitoring
```

# 2. Add Helm repositories
```
helm repo add grafana https://grafana.github.io/helm-charts
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
```

# 3. Deploy Prometheus + Grafana
```
helm install monitoring prometheus-community/kube-prometheus-stack \
  --version 72.6.2 \
  --namespace monitoring \
  --values helm/prometheus-stack-values.yaml \
  --wait
```

# 4. Deploy Tempo
```
helm install tempo grafana/tempo \
  --version 1.21.1 \
  --namespace monitoring \
  --values helm/tempo-values.yaml \
  --wait
```

# 5. Deploy Alloy
```
helm install alloy grafana/alloy \
  --version 1.0.3 \
  --namespace monitoring \
  --values helm/alloy-values.yaml \
  --wait
```

# 6. Deploy trace generator
```
kubectl apply -f trace-generator.yaml
```
