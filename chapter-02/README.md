# Chapter-01

## 2.2
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

Have a question, bug, or feature request? Let us know! https://kind.sigs.k8s.io/#community 🙂

❯ kind get clusters
kind

❯ kubectl cluster-info --context kind-kind
Kubernetes control plane is running at https://127.0.0.1:36323
CoreDNS is running at https://127.0.0.1:36323/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.

❯ kubectl get nodes
NAME                 STATUS   ROLES           AGE    VERSION
kind-control-plane   Ready    control-plane   2m8s   v1.29.0

❯ kind delete cluster
Deleting cluster "kind" ...
Deleted nodes: ["kind-control-plane"]

❯ kind get clusters
No kind clusters found.
```

##
```bash
```
