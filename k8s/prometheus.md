# Prometheus
```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
```
> add prometheus repo
```
helm show values prometheus-community/prometheus > values.yaml
```
> get values
```
  ...
  name: alertmanager
  ...
    storageClass: "nfs-client" # set sc
  ...
  name: server
  ...
    storageClass: "nfs-client" # set sc
  ...
```
> configure pronetheus (values.yaml)
```
helm install prometheus-community prometheus-community/prometheus -n monitoring --values values.yaml 
```
> install prometheus
```
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
```
> add grafana repo 
```
helm show values grafana/grafana > grafana-values.yaml
```
> get values
``` 
...
persistence:
  type: pvc
  enable: true
  storageClassName: nfs-client
...
initChownData:
  enabled: false
...
```
> configure values (grafana-values.yaml)
```
helm install -n monitoring grafana grafana/grafana --values grafana-values.yaml 
```
> install grafana
