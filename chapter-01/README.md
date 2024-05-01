# Chapter-01

## 1.2.5
```bash
❯ docker info
Client: Docker Engine - Community
 Version:    26.1.1
 Context:    default
 Debug Mode: false
 Plugins:
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.14.0
    Path:     /usr/libexec/docker/cli-plugins/docker-buildx
  compose: Docker Compose (Docker Inc.)
    Version:  v2.27.0
    Path:     /usr/libexec/docker/cli-plugins/docker-compose

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 26.1.1
 Storage Driver: overlay2
  Backing Filesystem: extfs
  Supports d_type: true
  Using metacopy: false
  Native Overlay Diff: true
  userxattr: false
 Logging Driver: json-file
 Cgroup Driver: systemd
 Cgroup Version: 2
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local splunk syslog
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: e377cd56a71523140ca6ae87e30244719194a521
 runc version: v1.1.12-0-g51d5e94
 init version: de40ad0
 Security Options:
  apparmor
  seccomp
   Profile: builtin
  cgroupns
 Kernel Version: 5.15.0-91-generic
 Operating System: Ubuntu 22.04.3 LTS
 OSType: linux
 Architecture: x86_64
 CPUs: 4
 Total Memory: 15.61GiB
 Name: bbf-kubernetes
 ID: f207dd4d-39b6-4622-bb71-8fc6c3e01db6
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Live Restore Enabled: false
```


## 1.2.6
```bash
❯ docker run --rm --detach --publish 8080:80 --name web nginx:1.25.3
Unable to find image 'nginx:1.25.3' locally
1.25.3: Pulling from library/nginx
e1caac4eb9d2: Pull complete
504c1e01744e: Pull complete
a1330b43d726: Pull complete
5e8995dba715: Pull complete
d5181593591e: Pull complete
74a4f808141d: Pull complete
330fd09f4306: Pull complete
Digest: sha256:c7a6ad68be85142c7fe1089e48faa1e7c7166a194caa9180ddea66345876b9d2
Status: Downloaded newer image for nginx:1.25.3
16997b05b8f53fbe3f1591b3d426f4a7299ca6440204345c9f5a777f6cbc5e03

❯ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                  NAMES
16997b05b8f5   nginx:1.25.3   "/docker-entrypoint.…"   34 seconds ago   Up 31 seconds   0.0.0.0:8080->80/tcp   web

❯ curl localhost:8080
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

## 1.2.9
```bash
❯  docker build ./chapter-01/custom-nginx --tag nginx-custom:1.0.0
[+] Building 0.9s (7/7) FINISHED                                                                  docker:default
 => [internal] load build definition from Dockerfile                                                        0.1s
 => => transferring dockerfile: 93B                                                                         0.0s
 => [internal] load metadata for docker.io/library/nginx:1.25.3                                             0.0s
 => [internal] load .dockerignore                                                                           0.1s
 => => transferring context: 2B                                                                             0.0s
 => [internal] load build context                                                                           0.2s
 => => transferring context: 59B                                                                            0.0s
 => [1/2] FROM docker.io/library/nginx:1.25.3                                                               0.3s
 => [2/2] COPY index.html /usr/share/nginx/html                                                             0.1s
 => exporting to image                                                                                      0.1s
 => => exporting layers                                                                                     0.1s
 => => writing image sha256:1a9729ebcf6219bf04fa0b5fb9498dec8649258db5970157ff1d072d24867dd6                0.0s
 => => naming to docker.io/library/nginx-custom:1.0.0

❯ docker images
REPOSITORY     TAG       IMAGE ID       CREATED          SIZE
nginx-custom   1.0.0     1a9729ebcf62   16 seconds ago   187MB
nginx          1.25.3    247f7abff9f7   6 months ago     187MB
```


## 1.2.10
```bash
❯ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                  NAMES
16997b05b8f5   nginx:1.25.3   "/docker-entrypoint.…"   14 minutes ago   Up 14 minutes   0.0.0.0:8080->80/tcp   web

❯ docker stop 16997b05b8f5
16997b05b8f5

❯ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

❯ docker run --rm --detach --publish 8080:80 --name web nginx-custom:1.0.0
9352b5b70e6f6e08df864ee827e68aecdb0c1619cf1d88473b3933cbea389c9a

❯ docker ps
CONTAINER ID   IMAGE                COMMAND                  CREATED         STATUS         PORTS                 NAMES
9352b5b70e6f   nginx-custom:1.0.0   "/docker-entrypoint.…"   3 seconds ago   Up 2 seconds   0.0.0.0:8080->80/tcp  web

❯ curl localhost:8080
<h1>Hello World!</h1>

❯ docker stop web
web

❯ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```


## 1.3
```bash
❯ cd chapter-01

❯ docker build ./hello-server --tag hello-server:1.0
[+] Building 99.7s (10/10) FINISHED                                                               docker:default
 => [internal] load build definition from Dockerfile                                                        0.0s
 => => transferring dockerfile: 198B                                                                        0.0s
 => [internal] load metadata for docker.io/library/golang:1.21                                              2.3s
 => [internal] load .dockerignore                                                                           0.0s
 => => transferring context: 2B                                                                             0.0s
 => [builder 1/4] FROM docker.io/library/golang:1.21@sha256:d83472f1ab5712a6b2b816dc811e46155e844ddc02f5f  58.7s
 => => resolve docker.io/library/golang:1.21@sha256:d83472f1ab5712a6b2b816dc811e46155e844ddc02f5f5952e72c6  0.0s
 => => sha256:d83472f1ab5712a6b2b816dc811e46155e844ddc02f5f5952e72c6deedafed77 2.13kB / 2.13kB              0.0s
 => => sha256:af2d3af00e57da762d0d6e1a95ea3aa594cd6173eab0a635b3322c673a9ef88a 2.88kB / 2.88kB              0.0s
 => => sha256:1468e7ff95fcb865fbc4dee7094f8b99c4dcddd6eb2180cf044c7396baf6fc2f 49.58MB / 49.58MB           19.7s
 => => sha256:c4c40c3e3cdf945721f480e1d939aac857876fdb5c33b8fbfcf655c63b0b9428 64.14MB / 64.14MB           37.9s
 => => sha256:758ddc9809127da6b2b2c143f2023a16a4636aa0e34db98dfc26bb4dd9e0d706 1.79kB / 1.79kB              0.0s
 => => sha256:2cf9c2b42f41b1845f3e4421b723d56146db82939dc884555e077768e18132f4 24.05MB / 24.05MB            9.6s
 => => sha256:18445a9ea386c08b9cd5a46a17c8099d961d6813c6f5945e2adeb24ba596456a 92.41MB / 92.41MB           42.0s
 => => sha256:c2c9e90aed829b7387fa3fa7121b7fda009a742719004ac50889a37665a5f08c 67.01MB / 67.01MB           45.8s
 => => extracting sha256:1468e7ff95fcb865fbc4dee7094f8b99c4dcddd6eb2180cf044c7396baf6fc2f                   4.6s
 => => extracting sha256:2cf9c2b42f41b1845f3e4421b723d56146db82939dc884555e077768e18132f4                   1.4s
 => => sha256:28752861b6df1c9aaf482c7b8dabcd98fdf77d6e722fa2dd82dfcddf0363158e 175B / 175B                 42.1s
 => => extracting sha256:c4c40c3e3cdf945721f480e1d939aac857876fdb5c33b8fbfcf655c63b0b9428                   5.5s
 => => sha256:4f4fb700ef54461cfa02571ae0db9a0dc1e0cdb5577484a6d75e68dc38e8acc1 32B / 32B                   42.4s
 => => extracting sha256:18445a9ea386c08b9cd5a46a17c8099d961d6813c6f5945e2adeb24ba596456a                   5.9s
 => => extracting sha256:c2c9e90aed829b7387fa3fa7121b7fda009a742719004ac50889a37665a5f08c                   8.2s
 => => extracting sha256:28752861b6df1c9aaf482c7b8dabcd98fdf77d6e722fa2dd82dfcddf0363158e                   0.0s
 => => extracting sha256:4f4fb700ef54461cfa02571ae0db9a0dc1e0cdb5577484a6d75e68dc38e8acc1                   0.0s
 => [internal] load build context                                                                           0.0s
 => => transferring context: 613B                                                                           0.0s
 => [builder 2/4] WORKDIR /app                                                                             19.9s
 => [builder 3/4] COPY . .                                                                                  0.1s
 => [builder 4/4] RUN go build -o hello .                                                                  18.0s
 => [stage-1 1/1] COPY --from=builder /app/hello /hello                                                     0.3s
 => exporting to image                                                                                      0.1s
 => => exporting layers                                                                                     0.1s
 => => writing image sha256:4cd92d89bb0302341e13e99e8c16a68ea475965091725da3c7ec191a61064c61                0.0s
 => => naming to docker.io/library/hello-server:1.0

❯ docker images hello-server
REPOSITORY     TAG       IMAGE ID       CREATED          SIZE
hello-server   1.0       4cd92d89bb03   44 seconds ago   6.72MB

❯ docker run --rm --detach --publish 8080:8080 --name hello-server hello-server:1.0
2b517c4f26288e64627664879e101cc469ecdf70ad92e3113fefaa9acd2d9918

❯ docker ps
CONTAINER ID   IMAGE              COMMAND    CREATED         STATUS         PORTS                    NAMES
2b517c4f2628   hello-server:1.0   "/hello"   5 seconds ago   Up 4 seconds   0.0.0.0:8080->8080/tcp   hello-server

❯ curl localhost:8080
Hello, world!%

❯ docker stop hello-server
hello-server

❯ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```
