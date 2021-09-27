# Taints and Tolerations
    kubectl taint node node1 key=value:NoSchedule 
> NoExecute - if pod exist on node, then it terminated

> NoSchedule - if pod exist on node, then it continues to running  
  
## Example yaml File
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
           operator: "Equal"
           effect: "NoSchedule"
    
> Correct for all value

