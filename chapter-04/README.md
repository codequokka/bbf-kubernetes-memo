# Chapter-04

## 4.2.1
```bash
❯ kind create cluster --image=kindest/node:v1.29.0
Creating cluster "kind" ...
 ✓ Ensuring node image (kindest/node:v1.29.0) 🖼
 ✓ Preparing nodes 📦
 ✓ Writing configuration 📜
 ✓ Starting control-plane 🕹
 ✓ Installing CNI 🔌
 ✓ Installing StorageClass 💾
Set kubectl context to "kind-kind"
You can now use your cluster with:

kubectl cluster-info --context kind-kind

Thanks for using kind! 😊

❯ kubectl get nodes
NAME                 STATUS     ROLES           AGE   VERSION
kind-control-plane   NotReady   control-plane   28s   v1.29.0

❯ kind get clusters
kind
```

## 4.2.3
```bash
❯ kubectl get pod --namespace default
No resources found in default namespace.

❯ kubectl apply --filename chapter-04/myapp.yaml --namespace default
pod/myapp created

❯ kubectl get pod --namespace default
NAME    READY   STATUS    RESTARTS   AGE
myapp   1/1     Running   0          27s
```
