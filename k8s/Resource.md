# Resource Requirements and Limits

    apiVersion: apps/v1
    kind: Deployment
    ...
	spec:
   	  ...
      template:
      ...
      spec:
        containers:
        - name: my-app
          image: nginx
          resources:
            limits:
              cpu: "1"
          requests:
              cpu: "0.5"
> defining cpu limits for containers

    apiVersion: apps/v1
    kind: Deployment
    ...
	spec:
   	  ...
      template:
      ...
      spec:
        containers:
        - name: my-app
          image: nginx
          resources:
            requests:
              memory: "128Mi"
            limits:
              memory: "256Mi"
> defining memory limits for containers