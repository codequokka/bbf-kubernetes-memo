# Chapter-01

## 1.2.5
- [README](../setup/README.md)の手順でVMを作成する
```bash
❯ lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 22.04.3 LTS
Release:        22.04
Codename:       jammy

❯ docker version
Client: Docker Engine - Community
 Version:           26.1.1
 API version:       1.45
 Go version:        go1.21.9
 Git commit:        4cf5afa
 Built:             Tue Apr 30 11:47:53 2024
 OS/Arch:           linux/amd64
 Context:           default

Server: Docker Engine - Community
 Engine:
  Version:          26.1.1
  API version:      1.45 (minimum version 1.24)
  Go version:       go1.21.9
  Git commit:       ac2de55
  Built:            Tue Apr 30 11:47:53 2024
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.6.31
  GitCommit:        e377cd56a71523140ca6ae87e30244719194a521
 runc:
  Version:          1.1.12
  GitCommit:        v1.1.12-0-g51d5e94
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
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
7ae42f9036858b14c16a39a67a33b1bc00f19a30fb570989ec16054cc1d64cb2

❯ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                  NAMES
7ae42f903685   nginx:1.25.3   "/docker-entrypoint.…"   17 seconds ago   Up 14 seconds   0.0.0.0:8080->80/tcp   web

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
❯ docker build ./chapter-01/custom-nginx --tag nginx-custom:1.0.0
[+] Building 0.9s (7/7) FINISHED                                                                  docker:default
 => [internal] load build definition from Dockerfile                                                        0.1s
 => => transferring dockerfile: 93B                                                                         0.0s
 => [internal] load metadata for docker.io/library/nginx:1.25.3                                             0.0s
 => [internal] load .dockerignore                                                                           0.1s
 => => transferring context: 2B                                                                             0.0s
 => [1/2] FROM docker.io/library/nginx:1.25.3                                                               0.3s
 => [internal] load build context                                                                           0.2s
 => => transferring context: 59B                                                                            0.0s
 => [2/2] COPY index.html /usr/share/nginx/html                                                             0.1s
 => exporting to image                                                                                      0.1s
 => => exporting layers                                                                                     0.1s
 => => writing image sha256:895d66d170a5eb449e3d716e07967868d5f222c2920be01f06bec13ecb4dabe5                0.0s
 => => naming to docker.io/library/nginx-custom:1.0.0                                                       0.0s

❯ docker images
REPOSITORY     TAG       IMAGE ID       CREATED         SIZE
nginx-custom   1.0.0     895d66d170a5   9 seconds ago   187MB
nginx          1.25.3    247f7abff9f7   6 months ago    187MB
```


## 1.2.10
```bash
❯ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                  NAMES
7ae42f903685   nginx:1.25.3   "/docker-entrypoint.…"   9 minutes ago   Up 9 minutes   0.0.0.0:8080->80/tcp   web

❯ docker stop 7ae42f903685
7ae42f903685

❯ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAME

❯ docker run --rm --detach --publish 8080:80 --name web nginx-custom:1.0.0
8bfaed8a1b7eb7f9d0be8992222ecf66718017d655e052d10a085aac13dbb4e8

❯ docker ps
CONTAINER ID   IMAGE                COMMAND                  CREATED         STATUS         PORTS                 NAMES
8bfaed8a1b7e   nginx-custom:1.0.0   "/docker-entrypoint.…"   3 seconds ago   Up 2 seconds   0.0.0.0:8080->80/tcp  web

❯ curl localhost:8080
<h1>Hello World!</h1>

❯ docker stop web
web

❯ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```


## 1.3
```bash
❯ docker build ./chapter-01/hello-server --tag hello-server:1.0
[+] Building 98.6s (10/10) FINISHED                                                               docker:default
 => [internal] load build definition from Dockerfile                                                        0.0s
 => => transferring dockerfile: 198B                                                                        0.0s
 => [internal] load metadata for docker.io/library/golang:1.21                                              2.4s
 => [internal] load .dockerignore                                                                           0.0s
 => => transferring context: 2B                                                                             0.0s
 => [builder 1/4] FROM docker.io/library/golang:1.21@sha256:d83472f1ab5712a6b2b816dc811e46155e844ddc02f5f  60.3s
 => => resolve docker.io/library/golang:1.21@sha256:d83472f1ab5712a6b2b816dc811e46155e844ddc02f5f5952e72c6  0.0s
 => => sha256:758ddc9809127da6b2b2c143f2023a16a4636aa0e34db98dfc26bb4dd9e0d706 1.79kB / 1.79kB              0.0s
 => => sha256:af2d3af00e57da762d0d6e1a95ea3aa594cd6173eab0a635b3322c673a9ef88a 2.88kB / 2.88kB              0.0s
 => => sha256:c4c40c3e3cdf945721f480e1d939aac857876fdb5c33b8fbfcf655c63b0b9428 64.14MB / 64.14MB           33.7s
 => => sha256:d83472f1ab5712a6b2b816dc811e46155e844ddc02f5f5952e72c6deedafed77 2.13kB / 2.13kB              0.0s
 => => sha256:2cf9c2b42f41b1845f3e4421b723d56146db82939dc884555e077768e18132f4 24.05MB / 24.05MB            6.8s
 => => sha256:1468e7ff95fcb865fbc4dee7094f8b99c4dcddd6eb2180cf044c7396baf6fc2f 49.58MB / 49.58MB           20.3s
 => => sha256:18445a9ea386c08b9cd5a46a17c8099d961d6813c6f5945e2adeb24ba596456a 92.41MB / 92.41MB           44.3s
 => => sha256:c2c9e90aed829b7387fa3fa7121b7fda009a742719004ac50889a37665a5f08c 67.01MB / 67.01MB           44.0s
 => => extracting sha256:1468e7ff95fcb865fbc4dee7094f8b99c4dcddd6eb2180cf044c7396baf6fc2f                   4.5s
 => => extracting sha256:2cf9c2b42f41b1845f3e4421b723d56146db82939dc884555e077768e18132f4                   1.4s
 => => extracting sha256:c4c40c3e3cdf945721f480e1d939aac857876fdb5c33b8fbfcf655c63b0b9428                   5.7s
 => => sha256:28752861b6df1c9aaf482c7b8dabcd98fdf77d6e722fa2dd82dfcddf0363158e 175B / 175B                 34.5s
 => => sha256:4f4fb700ef54461cfa02571ae0db9a0dc1e0cdb5577484a6d75e68dc38e8acc1 32B / 32B                   34.7s
 => => extracting sha256:18445a9ea386c08b9cd5a46a17c8099d961d6813c6f5945e2adeb24ba596456a                   5.7s
 => => extracting sha256:c2c9e90aed829b7387fa3fa7121b7fda009a742719004ac50889a37665a5f08c                   7.9s
 => => extracting sha256:28752861b6df1c9aaf482c7b8dabcd98fdf77d6e722fa2dd82dfcddf0363158e                   0.0s
 => => extracting sha256:4f4fb700ef54461cfa02571ae0db9a0dc1e0cdb5577484a6d75e68dc38e8acc1                   0.0s
 => [internal] load build context                                                                           0.0s
 => => transferring context: 613B                                                                           0.0s
 => [builder 2/4] WORKDIR /app                                                                             19.2s
 => [builder 3/4] COPY . .                                                                                  0.1s
 => [builder 4/4] RUN go build -o hello .                                                                  15.8s
 => [stage-1 1/1] COPY --from=builder /app/hello /hello                                                     0.3s
 => exporting to image                                                                                      0.1s
 => => exporting layers                                                                                     0.1s
 => => writing image sha256:c4d2c1f1e62cfe21f4af658a321937a6e02e2bcdec5d51e7dbad2696fc2a1273                0.0s
 => => naming to docker.io/library/hello-server:1.0                                                         0.0s

❯ docker images hello-server
REPOSITORY     TAG       IMAGE ID       CREATED          SIZE
hello-server   1.0       c4d2c1f1e62c   23 seconds ago   6.72MB

❯ docker run --rm --detach --publish 8080:8080 --name hello-server hello-server:1.0
0cecdbd21b54a9f4299863ccb1f91759d18446750a65adc7a4c8f065f6025185

❯ docker ps
CONTAINER ID   IMAGE              COMMAND    CREATED          STATUS          PORTS                    NAMES
0cecdbd21b54   hello-server:1.0   "/hello"   13 seconds ago   Up 13 seconds   0.0.0.0:8080->8080/tcp   hello-server

❯ curl localhost:8080
Hello, world!%

❯ docker stop hello-server
hello-server

❯ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```
