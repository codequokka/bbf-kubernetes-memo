# Errata

## Chapter-01

### 1.2.12
- Dockerfileのベストプラクティスのページのリンクが異なる
```
# 書面
https://docs.docker.com/reference/dockerfile/
```
```
# 実際
https://docs.docker.com/develop/develop-images/dockerfile_best-practices/

```

- 同梱されるバイナリ名が異なる
```
# 書面
マルチステージビルドを行うことで、このDockerイメージから起動されるコンテナではmainというバイナリのみ同梱されます。
```
```
# 実際
マルチステージビルドを行うことで、このDockerイメージから起動されるコンテナではhelloというバイナリのみ同梱されます。
```

### 1.3
- hello-serverコンテナのレスポンスの文字列が異なる
```bash
# 書面
$ curl localhost:8080
Hello, world! Let's learn Kubernetes!
```
```bash
# 実際
$ curl localhost:8080
Hello, world!%
```
