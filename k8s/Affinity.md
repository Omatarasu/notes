# Affinity
    kubectl label nodes node01 size=large
>  Add the label of the node01

## Example yaml Files
    apiVersion: apps/v1
    kind: Deployment
    ...
	spec:
   	  ...
      template:
      ...
      spec: 
        containers: 
        ... 
        affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
             nodeSelectorTerms:
             - matchExpressions:
               - key: size
                 operator: Exists 
> Correct for all value

    apiVersion: apps/v1
    kind: Deployment
    ...
	spec:
   	  ...
      template:
      ...
      spec: 
        containers: 
        ... 
        affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
             nodeSelectorTerms:
             - matchExpressions:
               - key: size
                 operator: In
                 values:
                 - large

> Can list values


