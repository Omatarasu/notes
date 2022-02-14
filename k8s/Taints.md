# Taints and Tolerations
### Apply Taint on node
```
kubectl taint node node1 key=value:NoSchedule 
OR
kubectl taint node node1 key=:NoSchedule
```
> NoExecute - if pod exist on node, then it terminated

> NoSchedule - if pod exist on node, then it continues to running  
### Remove Taint on node
```
kubectl taint node node1 key=value:NoSchedule-
```
  
## Example yaml Files
	apiVersion: apps/v1
    kind: Deployment
    ...
    spec:
       ...
       template:
         ...
         tolerations:
         - key: "key"
           value: "value"
           operator: "Equal"
           effect: "NoSchedule"
    
> Need to specify value

  	apiVersion: apps/v1
    kind: Deployment
    ...
    spec:
       ...
       template:
         ...
         tolerations:
         - key: "key"
           operator: "Exists"
           effect: "NoSchedule"
    
> Correct for all value

