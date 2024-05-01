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

Have a nice day! 👋

❯ docker images kindest/node
REPOSITORY     TAG       IMAGE ID       CREATED        SIZE
kindest/node   v1.29.0   dcd9d3cef648   4 months ago   912MB

❯ kind get clusters
kind

❯ kubectl cluster-info --context kind-kind
Kubernetes control plane is running at https://127.0.0.1:32777
CoreDNS is running at https://127.0.0.1:32777/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.

❯ kubectl version
Client Version: v1.30.0
Kustomize Version: v5.0.4-0.20230601165947-6ce0bf390ce3
Server Version: v1.29.0

❯ kind delete cluster
Deleting cluster "kind" ...
Deleted nodes: ["kind-control-plane"]

❯ kind get clusters
No kind clusters found.
```
