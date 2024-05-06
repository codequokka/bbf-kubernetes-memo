# Chapter-02

## 2.2
```bash
❯ source .envrc

❯ kubectl version
Client Version: v1.30.0
Kustomize Version: v5.0.4-0.20230601165947-6ce0bf390ce3
The connection to the server localhost:8080 was refused - did you specify the right host or port?

❯ kind version
kind v0.22.0 go1.20.13 linux/amd64

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

❯ docker images kindest/node
REPOSITORY     TAG       IMAGE ID       CREATED        SIZE
kindest/node   v1.29.0   dcd9d3cef648   4 months ago   912MB

❯ kind get clusters
kind

❯ docker images kindest/node
REPOSITORY     TAG       IMAGE ID       CREATED        SIZE
kindest/node   v1.29.0   dcd9d3cef648   4 months ago   912MB

❯ kubectl get nodes
NAME                 STATUS   ROLES           AGE     VERSION
kind-control-plane   Ready    control-plane   3m38s   v1.29.0

❯ kind delete cluster
Deleting cluster "kind" ...
Deleted nodes: ["kind-control-plane"]

❯ kind get clusters
No kind clusters found.
```
