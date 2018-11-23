# Linux에서  Golang 설치

##### 1. [golang Download page](https://golang.org/dl/)에서 Linux go~.tar.gz 다운로드

##### 2. 압축풀기

```shell
$ sudo tar -C /usr/local -xzf go1.4.2.linux-amd64.tar.gz 
```

##### 3. 환경변수 설정

**$ sudo vim /etc/profile** 맨 뒷 줄에

```
export PATH=$PATH:/usr/local/go/bin
```

##### 4. GOPATH 설정

* Golang root dir쯤 되는거 같다

**$ sudo vim /etc/profile** 맨 뒷줄에

```
export GOPATH=$HOME/WorkSpace/go
export PATH=$PATH:$GOPATH/bin
```

##### 5. go env로 확인!



# END

