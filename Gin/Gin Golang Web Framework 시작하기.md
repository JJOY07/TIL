# Gin: Golang Web Framework 시작하기

## 1. Installation

```shell
$ go get -u github.com/gin-gonic/gin
```

끝... ㅎ



### Govendor 설치

* 의존성관리를 해주는 Project manager

1. go get govendor

```shell
$ go get github.com/kardianos/govendor
```

2. project  폴더 생성 

```shell
$ mkdir -p $GOPATH/src/github.com/myusername/project && cd "$_"
```

3. project init && add in

```shell
$ govendor init
$ govendor fetch github.com/gin-gonic/gin@v1.3
```

4. 기본 template 복사

```shell
$ curl https://raw.githubusercontent.com/gin-gonic/gin/master/examples/basic/main.go > main.go
```

5. Project 시작

```shell
$ go run main.go
```



> 간단한 ping pong 웹 서버를 띄워볼 수 있다!  신기방기 :D

