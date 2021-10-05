# RBAC
	kube-apiserver --authorization-mode=RBAC ...
> enable RBAC on kube-apiserver

	apiVersion: rbac.authorization.k8s.io/v1
	kind: RoleBinding
	metadata:
  	  name: read-pods
  	  namespace: default
	subjects:
	- kind: User
      name: jane 
      apiGroup: rbac.authorization.k8s.io
	roleRef:
  	  kind: Role 
  	  name: pod-reader
  	  apiGroup: rbac.authorization.k8s.io
>  add jane to role pod-reader

> you can specify one or more subjects 

	apiVersion: rbac.authorization.k8s.io/v1
	kind: Role
	metadata:
  	  namespace: default
      name: pod-reader
    rules:
    - apiGroups: [""] # "" indicates the core API group
      resources: ["pods"]
      resourceName: ["my-pod", "my-pod-1"]  
      verbs: ["get", "watch", "list"]
> create Role pod-reader in default namespace

> allow only for pods my-pod and my-pod-1

	apiVersion: rbac.authorization.k8s.io/v1
	kind: ClusterRoleBinding
	metadata:	
  	  name: read-secrets-global
	subjects:
    - kind: Group
  	  name: manager 
      apiGroup: rbac.authorization.k8s.io
    roleRef:
      kind: ClusterRole
      name: secret-reader
      apiGroup: rbac.authorization.k8s.io
> add manager to role secret-reader



	apiVersion: rbac.authorization.k8s.io/v1
	kind: ClusterRole
	metadata:
  	  name: secret-reader
	rules:
	- apiGroups: [""]
      resources: ["secrets"]
      verbs: ["get", "watch", "list"]
> create ClusterRole secret-reader in all namespace

Role and Role Binding | ClusterRole and ClusterRoleBinding
  ---|---
in one namespace |   in all namespaces
