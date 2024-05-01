# Chapter-05

## 5.2.1
```bash
NAME     READY   STATUS    RESTARTS   AGE
myapp    1/1     Running   0          112m
myapp2   1/1     Running   0          39s

❯ kubectl get pod myapp --namespace default
NAME    READY   STATUS    RESTARTS   AGE
myapp   1/1     Running   0          113m

❯ kubectl get pod --output wide --namespace default
NAME     READY   STATUS    RESTARTS   AGE    IP           NODE                 NOMINATED NODE   READINESS GATES
myapp    1/1     Running   0          113m   10.244.0.5   kind-control-plane   <none>           <none>
myapp2   1/1     Running   0          106s   10.244.0.6   kind-control-plane   <none>           <none>

❯ kubectl get pod myapp --output yaml --namespace default
apiVersion: v1
kind: Pod
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","kind":"Pod","metadata":{"annotations":{},"labels":{"app":"myapp"},"name":"myapp","names
pace":"default"},"spec":{"containers":[{"image":"blux2/hello-server:1.0","name":"hello-server","ports":[{"contain
erPort":8080}]}]}}
  creationTimestamp: "2024-04-30T02:15:31Z"
  labels:
    app: myapp
  name: myapp
  namespace: default
  resourceVersion: "808"
  uid: 57b2f856-e049-45a9-bbb6-ed31f5c40ab0
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
      name: kube-api-access-r84hb
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
  - name: kube-api-access-r84hb
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
    lastTransitionTime: "2024-04-30T02:15:38Z"
    status: "True"
    type: PodReadyToStartContainers
  - lastProbeTime: null
    lastTransitionTime: "2024-04-30T02:15:31Z"
    status: "True"
    type: Initialized
  - lastProbeTime: null
    lastTransitionTime: "2024-04-30T02:15:38Z"
    status: "True"
    type: Ready
  - lastProbeTime: null
    lastTransitionTime: "2024-04-30T02:15:38Z"
    status: "True"
    type: ContainersReady
  - lastProbeTime: null
    lastTransitionTime: "2024-04-30T02:15:31Z"
    status: "True"
    type: PodScheduled
  containerStatuses:
  - containerID: containerd://cb66f87a4c9d08c1ce4dc1f756cb824fa917c816451f50f5dff7fd4a2f786c75
    image: docker.io/blux2/hello-server:1.0
    imageID: docker.io/blux2/hello-server@sha256:35ab584cbe96a15ad1fb6212824b3220935d6ac9d25b3703ba259973fac5697d
    lastState: {}
    name: hello-server
    ready: true
    restartCount: 0
    started: true
    state:
      running:
        startedAt: "2024-04-30T02:15:37Z"
  hostIP: 172.18.0.2
  hostIPs:
  - ip: 172.18.0.2
  phase: Running
  podIP: 10.244.0.5
  podIPs:
  - ip: 10.244.0.5
  qosClass: BestEffort
  startTime: "2024-04-30T02:15:31Z"

❯ kubectl get pod myapp --output yaml --namespace default > chapter-04/pod.yam

❯ diff -y chapter-04/pod.yaml chapter-04/myapp.yaml
apiVersion: v1                                                  apiVersion: v1
kind: Pod                                                       kind: Pod
metadata:                                                       metadata:
  annotations:                                                |   name: myapp
    kubectl.kubernetes.io/last-applied-configuration: |       <
      {"apiVersion":"v1","kind":"Pod","metadata":{"annotation <
  creationTimestamp: "2024-04-30T02:15:31Z"                   <
  labels:                                                         labels:
    app: myapp                                                      app: myapp
  name: myapp                                                 <
  namespace: default                                          <
  resourceVersion: "808"                                      <
  uid: 57b2f856-e049-45a9-bbb6-ed31f5c40ab0                   <
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
      name: kube-api-access-r84hb                             <
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
  - name: kube-api-access-r84hb                               <
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
    lastTransitionTime: "2024-04-30T02:15:38Z"                <
    status: "True"                                            <
    type: PodReadyToStartContainers                           <
  - lastProbeTime: null                                       <
    lastTransitionTime: "2024-04-30T02:15:31Z"                <
    status: "True"                                            <
    type: Initialized                                         <
  - lastProbeTime: null                                       <
    lastTransitionTime: "2024-04-30T02:15:38Z"                <
    status: "True"                                            <
    type: Ready                                               <
  - lastProbeTime: null                                       <
    lastTransitionTime: "2024-04-30T02:15:38Z"                <
    status: "True"                                            <
    type: ContainersReady                                     <
  - lastProbeTime: null                                       <
    lastTransitionTime: "2024-04-30T02:15:31Z"                <
    status: "True"                                            <
    type: PodScheduled                                        <
  containerStatuses:                                          <
  - containerID: containerd://cb66f87a4c9d08c1ce4dc1f756cb824 <
    image: docker.io/blux2/hello-server:1.0                   <
    imageID: docker.io/blux2/hello-server@sha256:35ab584cbe96 <
    lastState: {}                                             <
    name: hello-server                                        <
    ready: true                                               <
    restartCount: 0                                           <
    started: true                                             <
    state:                                                    <
      running:                                                <
        startedAt: "2024-04-30T02:15:37Z"                     <
  hostIP: 172.18.0.2                                          <
  hostIPs:                                                    <
  - ip: 172.18.0.2                                            <
  phase: Running                                              <
  podIP: 10.244.0.5                                           <
  podIPs:                                                     <
  - ip: 10.244.0.5                                            <
  qosClass: BestEffort                                        <
  startTime: "2024-04-30T02:15:31Z"                           <

❯ kubectl get pods myapp --output jsonpath='{.spec.containers[].image}' --namespace default
blux2/hello-server:1.0%

❯ kubectl get pods myapp --output json --namespace default | jq -r '.spec.containers[].image'
blux2/hello-server:1.0

❯ kubectl get pod myapp --v=7 --namespace default
I0430 04:20:05.301541  143985 loader.go:395] Config loaded from file:  /home/vagrant/.kube/config
I0430 04:20:05.307879  143985 round_trippers.go:463] GET https://127.0.0.1:41877/api/v1/namespaces/default/pods/m
yapp
I0430 04:20:05.308063  143985 round_trippers.go:469] Request Headers:
I0430 04:20:05.308086  143985 round_trippers.go:473]     Accept: application/json;as=Table;v=v1;g=meta.k8s.io,app
lication/json;as=Table;v=v1beta1;g=meta.k8s.io,application/json
I0430 04:20:05.308110  143985 round_trippers.go:473]     User-Agent: kubectl/v1.30.0 (linux/amd64) kubernetes/7c4
8c2b
I0430 04:20:05.321538  143985 round_trippers.go:574] Response Status: 200 OK in 13 milliseconds
NAME    READY   STATUS    RESTARTS   AGE
myapp   1/1     Running   0          124m

```

## 5.2.2
```bash
❯ kubectl describe pod myapp --namespace default
Name:             myapp
Namespace:        default
Priority:         0
Service Account:  default
Node:             kind-control-plane/172.18.0.2
Start Time:       Tue, 30 Apr 2024 02:15:31 +0000
Labels:           app=myapp
Annotations:      <none>
Status:           Running
IP:               10.244.0.5
IPs:
  IP:  10.244.0.5
Containers:
  hello-server:
    Container ID:   containerd://cb66f87a4c9d08c1ce4dc1f756cb824fa917c816451f50f5dff7fd4a2f786c75
    Image:          blux2/hello-server:1.0
    Image ID:       docker.io/blux2/hello-server@sha256:35ab584cbe96a15ad1fb6212824b3220935d6ac9d25b3703ba259973f
ac5697d
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 30 Apr 2024 02:15:37 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-r84hb (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True
  Initialized                 True
  Ready                       True
  ContainersReady             True
  PodScheduled                True
Volumes:
  kube-api-access-r84hb:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:                      <none>
```


## 5.2.3
```bash
❯ kubectl logs myapp --namespace default
2024/04/30 02:15:37 Starting server on port 8080

❯ kubectl logs myapp --container hello-server --namespace default
2024/04/30 02:15:37 Starting server on port 8080

❯ kubectl apply --filename chapter-05/myapp-label.yaml
pod/myapp3 created

❯ k get pods --namespace default
NAME     READY   STATUS    RESTARTS   AGE
myapp    1/1     Running   0          132m
myapp2   1/1     Running   0          20m
myapp3   1/1     Running   0          10s

❯ kubectl get pod --selector app=myapp
NAME     READY   STATUS    RESTARTS   AGE
myapp    1/1     Running   0          134m
myapp3   1/1     Running   0          94s

❯ kubectl logs --selector app=myapp
2024/04/30 02:15:37 Starting server on port 8080
2024/04/30 04:28:21 Starting server on port 8080
```

## 5.3.1
```bash
❯ kubectl debug --stdin --tty myapp --image=curlimages/curl:8.4.0 --target=hello-server --namespace default -- sh

Targeting container "hello-server". If you don't see processes from this container it may be because the containe
r runtime doesn't support this feature.
Defaulting debug container name to debugger-c8t45.
If you don't see a command prompt, try pressing enter.
~ $ curl localhost:8080
Hello, world!~ $ exit
Session ended, the ephemeral container will not be restarted but may be reattached using 'kubectl attach myapp -c
 debugger-c8t45 -i -t' if it is still running
```

## 5.3.2
```bash
❯ kubectl --namespace default run busybox --image=busybox:1.36.1 --rm --stdin --tty --restart=Never --command --
nslookup google.com
Server:         10.96.0.10
Address:        10.96.0.10:53

Non-authoritative answer:
Name:   google.com
Address: 172.217.31.174

Non-authoritative answer:
Name:   google.com
Address: 2404:6800:4004:801::200e

pod "busybox" deleted
```

## 5.3.3
```bash
❯ kubectl --namespace default run curlpod --image=curlimages/curl:8.4.0 --command -- /bin/sh -c "while true; do s
leep initify; done;"
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
Hello, world!~ $ exit
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
```
