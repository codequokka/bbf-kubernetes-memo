# Chapter-05

## 5.2.1
```bash
❯ kubectl run myapp2 --image=blux2/hello-server:1.0 --namespace default
pod/myapp2 created

❯ kubectl get pod --namespace default
NAME     READY   STATUS    RESTARTS   AGE
myapp    1/1     Running   0          4m1s
myapp2   1/1     Running   0          16s

❯ kubectl get pods myapp --namespace default
NAME    READY   STATUS    RESTARTS   AGE
myapp   1/1     Running   0          5m33s

❯ kubectl get pod --output wide --namespace default
NAME     READY   STATUS    RESTARTS   AGE     IP           NODE                 NOMINATED NODE   READINESS GATES
myapp    1/1     Running   0          5m53s   10.244.0.5   kind-control-plane   <none>           <none>
myapp2   1/1     Running   0          2m8s    10.244.0.6   kind-control-plane   <none>           <none>

❯ kubectl get pod myapp --output yaml --namespace default
apiVersion: v1
kind: Pod
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","kind":"Pod","metadata":{"annotations":{},"labels":{"app":"myapp"},"name":"myapp","names
pace":"default"},"spec":{"containers":[{"image":"blux2/hello-server:1.0","name":"hello-server","ports":[{"contain
erPort":8080}]}]}}
  creationTimestamp: "2024-05-01T04:43:18Z"
  labels:
    app: myapp
  name: myapp
  namespace: default
  resourceVersion: "696"
  uid: 6a8b1b2f-e679-4671-a4ef-acb3ffe7815e
spec:
  containers:
  - image: blux2/hello-server:1.0
    imagePullPolicy: IfNotPresent
    name: hello-server
    ports:
    - containerPort: 8080
      protocol: TCP
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-25nn2
      readOnly: true
  dnsPolicy: ClusterFirst
  enableServiceLinks: true
  nodeName: kind-control-plane
  preemptionPolicy: PreemptLowerPriority
  priority: 0
  restartPolicy: Always
  schedulerName: default-scheduler
  securityContext: {}
  serviceAccount: default
  serviceAccountName: default
  terminationGracePeriodSeconds: 30
  tolerations:
  - effect: NoExecute
    key: node.kubernetes.io/not-ready
    operator: Exists
    tolerationSeconds: 300
  - effect: NoExecute
    key: node.kubernetes.io/unreachable
    operator: Exists
    tolerationSeconds: 300
  volumes:
  - name: kube-api-access-25nn2
    projected:
      defaultMode: 420
      sources:
      - serviceAccountToken:
          expirationSeconds: 3607
          path: token
      - configMap:
          items:
          - key: ca.crt
            path: ca.crt
          name: kube-root-ca.crt
      - downwardAPI:
          items:
          - fieldRef:
              apiVersion: v1
              fieldPath: metadata.namespace
            path: namespace
status:
  conditions:
  - lastProbeTime: null
    lastTransitionTime: "2024-05-01T04:43:25Z"
    status: "True"
    type: PodReadyToStartContainers
  - lastProbeTime: null
    lastTransitionTime: "2024-05-01T04:43:18Z"
    status: "True"
    type: Initialized
  - lastProbeTime: null
    lastTransitionTime: "2024-05-01T04:43:25Z"
    status: "True"
    type: Ready
  - lastProbeTime: null
    lastTransitionTime: "2024-05-01T04:43:25Z"
    status: "True"
    type: ContainersReady
  - lastProbeTime: null
    lastTransitionTime: "2024-05-01T04:43:18Z"
    status: "True"
    type: PodScheduled
  containerStatuses:
  - containerID: containerd://23bca91efb75384512393d6736dadb341de55db6f12587eb8d703c0be38b3043
    image: docker.io/blux2/hello-server:1.0
    imageID: docker.io/blux2/hello-server@sha256:35ab584cbe96a15ad1fb6212824b3220935d6ac9d25b3703ba259973fac5697d
    lastState: {}
    name: hello-server
    ready: true
    restartCount: 0
    started: true
    state:
      running:
        startedAt: "2024-05-01T04:43:25Z"
  hostIP: 172.18.0.2
  hostIPs:
  - ip: 172.18.0.2
  phase: Running
  podIP: 10.244.0.5
  podIPs:
  - ip: 10.244.0.5
  qosClass: BestEffort
  startTime: "2024-05-01T04:43:18Z"

❯ kubectl get pod myapp --output yaml --namespace default > chapter-05/pod.yaml

❯ diff -y chapter-05/pod.yaml chapter-04/myapp.yaml
apiVersion: v1                                                  apiVersion: v1
kind: Pod                                                       kind: Pod
metadata:                                                       metadata:
  annotations:                                                |   name: myapp
    kubectl.kubernetes.io/last-applied-configuration: |       <
      {"apiVersion":"v1","kind":"Pod","metadata":{"annotation <
  creationTimestamp: "2024-05-01T04:43:18Z"                   <
  labels:                                                         labels:
    app: myapp                                                      app: myapp
  name: myapp                                                 <
  namespace: default                                          <
  resourceVersion: "696"                                      <
  uid: 6a8b1b2f-e679-4671-a4ef-acb3ffe7815e                   <
spec:                                                           spec:
  containers:                                                     containers:
  - image: blux2/hello-server:1.0                             |     - name: hello-server
    imagePullPolicy: IfNotPresent                             |       image: blux2/hello-server:1.0
    name: hello-server                                        |       ports:
    ports:                                                    |         - containerPort: 8080
    - containerPort: 8080                                     <
      protocol: TCP                                           <
    resources: {}                                             <
    terminationMessagePath: /dev/termination-log              <
    terminationMessagePolicy: File                            <
    volumeMounts:                                             <
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccoun <
      name: kube-api-access-25nn2                             <
      readOnly: true                                          <
  dnsPolicy: ClusterFirst                                     <
  enableServiceLinks: true                                    <
  nodeName: kind-control-plane                                <
  preemptionPolicy: PreemptLowerPriority                      <
  priority: 0                                                 <
  restartPolicy: Always                                       <
  schedulerName: default-scheduler                            <
  securityContext: {}                                         <
  serviceAccount: default                                     <
  serviceAccountName: default                                 <
  terminationGracePeriodSeconds: 30                           <
  tolerations:                                                <
  - effect: NoExecute                                         <
    key: node.kubernetes.io/not-ready                         <
    operator: Exists                                          <
    tolerationSeconds: 300                                    <
  - effect: NoExecute                                         <
    key: node.kubernetes.io/unreachable                       <
    operator: Exists                                          <
    tolerationSeconds: 300                                    <
  volumes:                                                    <
  - name: kube-api-access-25nn2                               <
    projected:                                                <
      defaultMode: 420                                        <
      sources:                                                <
      - serviceAccountToken:                                  <
          expirationSeconds: 3607                             <
          path: token                                         <
      - configMap:                                            <
          items:                                              <
          - key: ca.crt                                       <
            path: ca.crt                                      <
          name: kube-root-ca.crt                              <
      - downwardAPI:                                          <
          items:                                              <
          - fieldRef:                                         <
              apiVersion: v1                                  <
              fieldPath: metadata.namespace                   <
            path: namespace                                   <
status:                                                       <
  conditions:                                                 <
  - lastProbeTime: null                                       <
    lastTransitionTime: "2024-05-01T04:43:25Z"                <
    status: "True"                                            <
    type: PodReadyToStartContainers                           <
  - lastProbeTime: null                                       <
    lastTransitionTime: "2024-05-01T04:43:18Z"                <
    status: "True"                                            <
    type: Initialized                                         <
  - lastProbeTime: null                                       <
    lastTransitionTime: "2024-05-01T04:43:25Z"                <
    status: "True"                                            <
    type: Ready                                               <
  - lastProbeTime: null                                       <
    lastTransitionTime: "2024-05-01T04:43:25Z"                <
    status: "True"                                            <
    type: ContainersReady                                     <
  - lastProbeTime: null                                       <
    lastTransitionTime: "2024-05-01T04:43:18Z"                <
    status: "True"                                            <
    type: PodScheduled                                        <
  containerStatuses:                                          <
  - containerID: containerd://23bca91efb75384512393d6736dadb3 <
    image: docker.io/blux2/hello-server:1.0                   <
    imageID: docker.io/blux2/hello-server@sha256:35ab584cbe96 <
    lastState: {}                                             <
    name: hello-server                                        <
    ready: true                                               <
    restartCount: 0                                           <
    started: true                                             <
    state:                                                    <
      running:                                                <
        startedAt: "2024-05-01T04:43:25Z"                     <
  hostIP: 172.18.0.2                                          <
  hostIPs:                                                    <
  - ip: 172.18.0.2                                            <
  phase: Running                                              <
  podIP: 10.244.0.5                                           <
  podIPs:                                                     <
  - ip: 10.244.0.5                                            <
  qosClass: BestEffort                                        <
  startTime: "2024-05-01T04:43:18Z"                           <


❯ kubectl get pods myapp --output jsonpath='{.spec.containers[].image}' --namespace default
blux2/hello-server:1.0%

❯ kubectl get pods myapp --output json --namespace default | jq -r '.spec.containers[].image'
blux2/hello-server:1.0

❯ kubectl get pod myapp --v=7 --namespace default
I0501 04:53:51.068261   76616 loader.go:395] Config loaded from file:  /home/vagrant/.kube/config
I0501 04:53:51.075333   76616 round_trippers.go:463] GET https://127.0.0.1:35199/api/v1/namespaces/default/pods/m
yapp
I0501 04:53:51.075374   76616 round_trippers.go:469] Request Headers:
I0501 04:53:51.075388   76616 round_trippers.go:473]     Accept: application/json;as=Table;v=v1;g=meta.k8s.io,app
lication/json;as=Table;v=v1beta1;g=meta.k8s.io,application/json
I0501 04:53:51.075397   76616 round_trippers.go:473]     User-Agent: kubectl/v1.30.0 (linux/amd64) kubernetes/7c4
8c2b
I0501 04:53:51.089442   76616 round_trippers.go:574] Response Status: 200 OK in 14 milliseconds
NAME    READY   STATUS    RESTARTS   AGE
myapp   1/1     Running   0          10m
```

## 5.2.2
```bash
❯ kubectl describe pod myapp --namespace default
Name:             myapp
Namespace:        default
Priority:         0
Service Account:  default
Node:             kind-control-plane/172.18.0.2
Start Time:       Wed, 01 May 2024 04:43:18 +0000
Labels:           app=myapp
Annotations:      <none>
Status:           Running
IP:               10.244.0.5
IPs:
  IP:  10.244.0.5
Containers:
  hello-server:
    Container ID:   containerd://23bca91efb75384512393d6736dadb341de55db6f12587eb8d703c0be38b3043
    Image:          blux2/hello-server:1.0
    Image ID:       docker.io/blux2/hello-server@sha256:35ab584cbe96a15ad1fb6212824b3220935d6ac9d25b3703ba259973f
ac5697d
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Wed, 01 May 2024 04:43:25 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-25nn2 (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True
  Initialized                 True
  Ready                       True
  ContainersReady             True
  PodScheduled                True
Volumes:
  kube-api-access-25nn2:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  11m   default-scheduler  Successfully assigned default/myapp to kind-control-plane
  Normal  Pulling    11m   kubelet            Pulling image "blux2/hello-server:1.0"
  Normal  Pulled     11m   kubelet            Successfully pulled image "blux2/hello-server:1.0" in 5.392s (5.392s including waiting)
  Normal  Created    11m   kubelet            Created container hello-server
  Normal  Started    11m   kubelet            Started container hello-server
```


## 5.2.3
```bash
❯ kubectl logs myapp --namespace default
2024/05/01 04:43:25 Starting server on port 8080

❯ kubectl logs myapp --container hello-server --namespace default
2024/05/01 04:43:25 Starting server on port 8080

❯ kubectl logs deployments/hello-server
error: error from server (NotFound): deployments.apps "hello-server" not found in namespace "default"

❯ kubectl apply --filename chapter-05/myapp-label.yaml
pod/myapp3 created

❯ kubectl get pods --namespace default
NAME     READY   STATUS    RESTARTS   AGE
myapp    1/1     Running   0          14m
myapp2   1/1     Running   0          10m
myapp3   1/1     Running   0          11s

❯ kubectl get pod --selector app=myapp
NAME     READY   STATUS    RESTARTS   AGE
myapp    1/1     Running   0          16m
myapp3   1/1     Running   0          2m2s

❯ kubectl logs --selector app=myapp
2024/05/01 04:43:25 Starting server on port 8080
2024/05/01 04:57:41 Starting server on port 8080
```

## 5.3.1
```bash
❯ kubectl debug --stdin --tty myapp --image=curlimages/curl:8.4.0 --target=hello-server --namespace default -- sh

Targeting container "hello-server". If you don't see processes from this container it may be because the containe
r runtime doesn't support this feature.
Defaulting debug container name to debugger-p58ck.
If you don't see a command prompt, try pressing enter.
~ $ curl localhost:8080
Hello, world!~ $
~ $ exit
Session ended, the ephemeral container will not be restarted but may be reattached using 'kubectl attach myapp -c
 debugger-p58ck -i -t' if it is still running
```

## 5.3.2
```bash
❯ kubectl --namespace default run busybox --image=busybox:1.36.1 --rm --stdin --tty --restart=Never --command --
nslookup google.com
Server:         10.96.0.10
Address:        10.96.0.10:53

Non-authoritative answer:
Name:   google.com
Address: 2404:6800:4004:823::200e

Non-authoritative answer:
Name:   google.com
Address: 142.250.196.142

pod "busybox" deleted
```

## 5.3.3
```bash
❯ kubectl --namespace default run curlpod --image=curlimages/curl:8.4.0 --command -- /bin/sh -c "while true; do sleep initify; done;"
pod/curlpod created

❯ kubectl get pod --namespace default
NAME      READY   STATUS    RESTARTS   AGE
curlpod   1/1     Running   0          13s
myapp     1/1     Running   0          141m
myapp2    1/1     Running   0          29m
myapp3    1/1     Running   0          8m26s

❯ kubectl get pod myapp --output wide --namespace default
NAME    READY   STATUS    RESTARTS   AGE    IP           NODE                 NOMINATED NODE   READINESS GATES
myapp   1/1     Running   0          141m   10.244.0.5   kind-control-plane   <none>           <none>

❯ kubectl --namespace default exec --stdin --tty curlpod -- /bin/sh
~ $ curl 10.244.0.5:8080
Hello, world!~ $
~ $ exit
```

## 5.3.4
```bash
❯ kubectl port-forward myapp 5555:8080 --namespace default
Forwarding from 127.0.0.1:5555 -> 8080
^Z
zsh: suspended  kubectl port-forward myapp 5555:8080 --namespace default

❯ bg
[1]  + continued  kubectl port-forward myapp 5555:8080 --namespace default

❯ curl localhost:5555
Handling connection for 5555
Hello, world!%

❯ fg
[1]  + running    kubectl port-forward myapp 5555:8080 --namespace default
^C%
```


## 5.4.1
```bash
❯ kubectl edit pod myapp --namespace default
pod/myapp edited

❯ kubectl get pods myapp --output jsonpath='{.metadata.labels}' --namespace default
{"app":"myapp","env":"prod"}%
```


## 5.4.2
```bash
❯ kubectl get pod --namespace default
NAME      READY   STATUS    RESTARTS   AGE
curlpod   1/1     Running   0          7m45s
myapp     1/1     Running   0          38m
myapp2    1/1     Running   0          34m
myapp3    1/1     Running   0          23m

❯ kubectl delete pod myapp --namespace default
pod "myapp" deleted

❯ kubectl get pod --namespace default
NAME      READY   STATUS    RESTARTS   AGE
curlpod   1/1     Running   0          8m4s
myapp2    1/1     Running   0          34m
myapp3    1/1     Running   0          24m

❯ kubectl delete pod curlpod myapp2 myapp3 --namespace default
pod "curlpod" deleted
pod "myapp2" deleted
pod "myapp3" deleted

❯ kubectl get pod --namespace default
No resources found in default namespace.
```

## 5.5.3
```bash
❯ kubectl api-resources
NAME                              SHORTNAMES   APIVERSION                        NAMESPACED   KIND
bindings                                       v1                                true         Binding
componentstatuses                 cs           v1                                false        ComponentStatus
configmaps                        cm           v1                                true         ConfigMap
endpoints                         ep           v1                                true         Endpoints
events                            ev           v1                                true         Event
limitranges                       limits       v1                                true         LimitRange
namespaces                        ns           v1                                false        Namespace
nodes                             no           v1                                false        Node
persistentvolumeclaims            pvc          v1                                true         PersistentVolumeCla
im
persistentvolumes                 pv           v1                                false        PersistentVolume
pods                              po           v1                                true         Pod
podtemplates                                   v1                                true         PodTemplate
replicationcontrollers            rc           v1                                true         ReplicationControll
er
resourcequotas                    quota        v1                                true         ResourceQuota
secrets                                        v1                                true         Secret
serviceaccounts                   sa           v1                                true         ServiceAccount
services                          svc          v1                                true         Service
mutatingwebhookconfigurations                  admissionregistration.k8s.io/v1   false        MutatingWebhookConf
iguration
validatingwebhookconfigurations                admissionregistration.k8s.io/v1   false        ValidatingWebhookCo
nfiguration
customresourcedefinitions         crd,crds     apiextensions.k8s.io/v1           false        CustomResourceDefin
ition
apiservices                                    apiregistration.k8s.io/v1         false        APIService
controllerrevisions                            apps/v1                           true         ControllerRevision
daemonsets                        ds           apps/v1                           true         DaemonSet
deployments                       deploy       apps/v1                           true         Deployment
replicasets                       rs           apps/v1                           true         ReplicaSet
statefulsets                      sts          apps/v1                           true         StatefulSet
selfsubjectreviews                             authentication.k8s.io/v1          false        SelfSubjectReview
tokenreviews                                   authentication.k8s.io/v1          false        TokenReview
localsubjectaccessreviews                      authorization.k8s.io/v1           true         LocalSubjectAccessR
eview
selfsubjectaccessreviews                       authorization.k8s.io/v1           false        SelfSubjectAccessRe
view
selfsubjectrulesreviews                        authorization.k8s.io/v1           false        SelfSubjectRulesRev
iew
subjectaccessreviews                           authorization.k8s.io/v1           false        SubjectAccessReview
horizontalpodautoscalers          hpa          autoscaling/v2                    true         HorizontalPodAutosc
aler
cronjobs                          cj           batch/v1                          true         CronJob
jobs                                           batch/v1                          true         Job
certificatesigningrequests        csr          certificates.k8s.io/v1            false        CertificateSigningR
equest
leases                                         coordination.k8s.io/v1            true         Lease
endpointslices                                 discovery.k8s.io/v1               true         EndpointSlice
events                            ev           events.k8s.io/v1                  true         Event
flowschemas                                    flowcontrol.apiserver.k8s.io/v1   false        FlowSchema
prioritylevelconfigurations                    flowcontrol.apiserver.k8s.io/v1   false        PriorityLevelConfig
uration
ingressclasses                                 networking.k8s.io/v1              false        IngressClass
ingresses                         ing          networking.k8s.io/v1              true         Ingress
networkpolicies                   netpol       networking.k8s.io/v1              true         NetworkPolicy
runtimeclasses                                 node.k8s.io/v1                    false        RuntimeClass
poddisruptionbudgets              pdb          policy/v1                         true         PodDisruptionBudget
clusterrolebindings                            rbac.authorization.k8s.io/v1      false        ClusterRoleBinding
clusterroles                                   rbac.authorization.k8s.io/v1      false        ClusterRole
rolebindings                                   rbac.authorization.k8s.io/v1      true         RoleBinding
roles                                          rbac.authorization.k8s.io/v1      true         Role
priorityclasses                   pc           scheduling.k8s.io/v1              false        PriorityClass
csidrivers                                     storage.k8s.io/v1                 false        CSIDriver
csinodes                                       storage.k8s.io/v1                 false        CSINode
csistoragecapacities                           storage.k8s.io/v1                 true         CSIStorageCapacity
storageclasses                    sc           storage.k8s.io/v1                 false        StorageClass
volumeattachments                              storage.k8s.io/v1                 false        VolumeAttachment
```
