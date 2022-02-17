# Ingress Controller Nginx
```
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
```
> add repo (ingress-nginx - any value)
```
helm show values ingress-nginx/ingress-nginx > values.yaml
```
> download values
```
kubectl label nodes  node4 node-role.kubernetes.io/ingress=""
kubectl taint nodes node4 node-role.kubernetes.io/ingress=:NoSchedule
```
> set taint and label
```
...
  hostNetwork: true
  hostPort:
    enabled: true
    ports:   
      http: 80
      https: 443
...
  tolerations:
    - key: "node-role.kubernetes.io/ingress"
      operator: "Exists"
      effect: "NoSchedule"
...
  nodeSelector:
    node-role.kubernetes.io/ingress: ""
...
```
> configure ingress controller (values.yaml)
```
kubectl create ns ingress-nginx
helm install ingress-nginx ingress-nginx/ingress-nginx --namespace ingress-nginx --values values.yaml 
```
> install ingress controller
