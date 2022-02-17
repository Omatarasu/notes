# NFS auto pv
```
helm repo add nfs-subdir-external-provisioner https://kubernetes-sigs.github.io/nfs-subdir-external-provisioner
helm repo update
```
> Add nfs-providioner repo
```
helm show values nfs-subdir-external-provisioner/nfs-subdir-external-provisioner > values.yaml
```
> Get values
```
...
nfs:
  server: 10.0.10.30 # address of the server
  path: /mnt/nfs/k8s # path on server
...
```
> configure nfs-provisioner (values.yaml)
```
helm install nfs-subdir-external-provisioner/nfs-subdir-external-provisioner --values values.yaml
```
> install nfs-provisioner
```
apiVersion: v1
kind: PersistentVolumeClaim 
metadata: 
  name: my-pvc
spec:
  storageClassName: nfs-client # use nfs provisioner
  accessModes:
    - ReadWriteOnce
  resources:
    requests:  
      storage: 1Gi
```
> create test pvc.yaml
```
kubectl apply -f pvc.yaml
```
> apply test pvc yaml
```
kubectl get pvc 
kubectl get pv
kubectl get sc
```
> test all 
