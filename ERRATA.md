# Errata

## Chapter-01

### 1.2.12
- helloというバイナリが同梱される
```
マルチステージビルドを行うことで、このDockerイメージから起動されるコンテナではmainというバイナリのみ同梱されます。
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
Hello, world!
```
