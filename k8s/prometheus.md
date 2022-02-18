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
  nodeExporter:
  ...
    tolerations: # tolerations to master and ingress
    - key: "node-role.kubernetes.io/master"
      operator: "Exists"
      effect: "NoSchedule"
    - key: "node-role.kubernetes.io/ingress"
      operator: "Exists"
      effect: "NoSchedule"
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
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-grafana
  labels:
    name: ingress-grafana
spec:
  ingressClassName: nginx
  rules:
  - host: grafana.k8s.local
    http:
      paths:
      - pathType: Prefix
        path: "/"
        backend:
          service:
            name: grafana
            port: 
              number: 80
```
> ingrass-grafana.yaml
```
kubectl apply -f ingress-grafana.yaml
```
> start ingress
```
kubectl get secret --namespace monitoring grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```
> get grafana pssword
###Login to grafana web https://grafana.k8s.local. use admin login. connect prometheus
