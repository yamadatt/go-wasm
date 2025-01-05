golangでwasmを動かしてみる

##　前提

wasiで動かす場合、前提としてwasmtimeが導入してあること。

以下、インストール手順。

https://wasmtime.dev/


##　動かし方

### 実行環境にJavaScript

コンパイルして、main.wasmを作る。

```bash
GOOS=js GOARCH=wasm go build -o main.wasm main.go
```

nginxを動かす。

```bash
docker run --rm --name webtest -v $(pwd):/usr/share/nginx/html:ro -p 8080:80 nginx:latest
```

以下のように8080ポートにアクセスする。IPアドレスは任意。

```bash
http://192.168.1.78:8080/index.html
```

### 実行環境をWASIにして動かす

```GOOS=wasip1```でコンパイルする。

```bash
GOOS=wasip1 GOARCH=wasm go build -o main.wasm
```

動かす。

```bash
wasmtime main.wasm 
```

