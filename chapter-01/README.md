# Chapter-01

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
c85abe44fd3c1dae0e8f359d187349f3c4235cdf2970eca1aa5148065281c339

❯ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                  NAME
S
c85abe44fd3c   nginx:1.25.3   "/docker-entrypoint.…"   3 minutes ago   Up 3 minutes   0.0.0.0:8080->80/tcp   web

❯ curl http://localhost:8080
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
</html
```

## 1.2.9
```bash
❯ docker build ./chapter-01/custom-nginx --tag nginx-custom:1.0.0
[+] Building 0.2s (7/7) FINISHED                                                                  docker:default
 => [internal] load build definition from Dockerfile                                                        0.0s
 => => transferring dockerfile: 93B                                                                         0.0s
 => [internal] load metadata for docker.io/library/nginx:1.25.3                                             0.0s
 => [internal] load .dockerignore                                                                           0.0s
 => => transferring context: 2B                                                                             0.0s
 => [internal] load build context                                                                           0.0s
 => => transferring context: 31B                                                                            0.0s
 => [1/2] FROM docker.io/library/nginx:1.25.3                                                               0.0s
 => CACHED [2/2] COPY index.html /usr/share/nginx/html                                                      0.0s
 => exporting to image                                                                                      0.0s
 => => exporting layers                                                                                     0.0s
 => => writing image sha256:c4ac98096f6f7d322cf43e84a218924d30f1e1142cdcd3d65e8347dc5757b56e                0.0s
 => => naming to docker.io/library/nginx-custom:1.0.0

❯ docker images
REPOSITORY     TAG       IMAGE ID       CREATED         SIZE
nginx-custom   1.0.0     c4ac98096f6f   6 minutes ago   187MB
nginx          1.25.3    247f7abff9f7   6 months ago    187MB
```

## 1.2.10
```bash
❯ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                  NA
MES
c85abe44fd3c   nginx:1.25.3   "/docker-entrypoint.…"   21 minutes ago   Up 21 minutes   0.0.0.0:8080->80/tcp   we
b

❯ docker stop c85abe44fd3c
c85abe44fd3c

❯ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

❯ docker run --rm --detach --publish 8080:80 --name web nginx-custom:1.0.0
9d33d88cf3af5bf55904c154bafeb5692338dfa08e6f7c529045d431fb906129

❯ docker ps
CONTAINER ID   IMAGE                COMMAND                  CREATED         STATUS         PORTS
  NAMES
9d33d88cf3af   nginx-custom:1.0.0   "/docker-entrypoint.…"   5 seconds ago   Up 4 seconds   0.0.0.0:8080->80/tcp
  web

❯ curl http://localhost:8080
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
[+] Building 19.0s (10/10) FINISHED                                                               docker:default
 => [internal] load build definition from Dockerfile                                                        0.0s
 => => transferring dockerfile: 198B                                                                        0.0s
 => [internal] load metadata for docker.io/library/golang:1.21                                              1.8s
 => [internal] load .dockerignore                                                                           0.0s
 => => transferring context: 2B                                                                             0.0s
 => [builder 1/4] FROM docker.io/library/golang:1.21@sha256:d83472f1ab5712a6b2b816dc811e46155e844ddc02f5f5  0.0s
 => [internal] load build context                                                                           0.0s
 => => transferring context: 395B                                                                           0.0s
 => CACHED [builder 2/4] WORKDIR /app                                                                       0.0s
 => [builder 3/4] COPY . .                                                                                  0.1s
 => [builder 4/4] RUN go build -o hello .                                                                  16.4s
 => [stage-1 1/1] COPY --from=builder /app/hello /hello                                                     0.3s
 => exporting to image                                                                                      0.2s
 => => exporting layers                                                                                     0.1s
 => => writing image sha256:0fa062c3becbf3e6d0bf1a7ccce8d198996454333335a93414e92689142d7385                0.0s
 => => naming to docker.io/library/hello-server:1.0                                                         0.0s

❯ docker images hello-server
REPOSITORY     TAG       IMAGE ID       CREATED          SIZE
hello-server   1.0       0fa062c3becb   59 seconds ago   6.72MB

❯ docker run --rm --detach --publish 8080:8080 --name hello-server hello-server:1.0
0d06f3266a361fbaf0c32a8ea80f56f0c5528563e6876f14c7708e57abdedce5

❯ docker ps
CONTAINER ID   IMAGE              COMMAND    CREATED         STATUS         PORTS                    NAMES
0d06f3266a36   hello-server:1.0   "/hello"   6 seconds ago   Up 5 seconds   0.0.0.0:8080->8080/tcp   hello-server

❯ curl localhost:8080
Hello, world!%

❯ docker stop hello-server
hello-server

❯ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```




```bash
```
```bash
```
