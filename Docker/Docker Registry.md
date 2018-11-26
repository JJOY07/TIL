# Docker Registry

* docker image를 저장하고 배포할 수 있는 저장소

* Docker Hub에서 pull, push로 image를 올리고 받아올 수 있음

* tag별로 관리도 할 수 있음

* Docker Registry server에 image를 저장하는 방법!

  * Registry가 있는 서버에 저장! (아래 "간단하게 사용해보자"는 local에 registry container를 띄워서 실습해봄)
  * cloud 환경 (Amazon S3, MS Azure, OpenStack Swift 등등)
  * 다른 storage back-end를 사용하고 싶다면 API 직접 구현


### 왜 써야하는가?

* 환경 구축을 해놓은 후, image를 저장해 놓으면 그 다음번엔 image를 받아오기만 하면됨
* 이 image는 사내에서 배포할 때 또는 환경 구축할 때 쓰면 짱짱
* image 관리하기도 편하다 (github가 얼마나 편한지 생각하면 되려나?)



### 간단하게 사용해보자

##### 1. Docker Hub를 통해 Docker registry image 받기

```shell
$ sudo docker pull registry:latest
```

##### 2. image를 컨테이너로 실행

```shell
$ sudo docker run -d -p 5000:5000 --name hello-registry -v /tmp/registry:/tmp/registry registry
```

* **--name [ps name]**: container name 지정
* **-d**: back ground에서 실행
* **-p [host port:container port]**: container port가 host port에 노출
* **-v [host img 파일 저장경로]:[컨테이너 저장경로]**
* **실행하려는 image name**: 여기서는 registry
* ![img](http://www.pyrasis.com/assets/images/DockerForTheReallyImpatientChapter06/1.png)

##### 3. 개인 저장소에 image 올리기

* 꼭 tag를 먼저 생성해야한다!

  **docker tag <image name>:<tag> <Docker registry URL>/<image name>: <tag>**

  ```shell
  $ sudo docker tag hello:0.1 localhost:5000/hello:0.1
  ```

* push로 image 올리기

  **docker push <Docker Registry URL>/<image name>:<tag>**

  ```shell
  $ sudo docker push localhost:5000/hello:0.1
  ```



##### 4. pull로 registry image 받아오기

**docker pull <Docker Registry URL>/<image name>:<tag>**

```shell
$ sudo docker pull localhost:5000/hello:0.1
```

> 내가 올린 이미지가 딱 생겼다!



##### 5. 다시 지우자 ^_^

```shell
$ sudo docker rmi localhost:5000/hello:0.1
```



### Amazone S3에 올려보자

* **-e** 옵션 사용

```shell
$ sudo docker run -d -p 5000:5000 --name s3-registry \
    -e SETTINGS_FLAVOR=s3 \
    -e AWS_BUCKET=examplebucket10 \
    -e STORAGE_PATH=/registry \
    -e AWS_KEY=AKIABCDEFGHIJKLMNOPQ \
    -e AWS_SECRET=sF4321ABCDEFGHIJKLMNOPqrstuvwxyz21345Afc \ registry
```

* **SETTING_FLAVOR**: 이미지 저장방법 (여기선 S3)

* **AWS_BUCKET**: 이미지를 저장할 S3 버킷 이름

* **STORAGE_PATH**: 이미지 데이터 저장 경로

* **AWS_KEY**: AWS 액세스 키

* **AWS_SECRET**: AWS secret 키

* s3-registry 저장소에 push

* ![img](http://www.pyrasis.com/assets/images/DockerForTheReallyImpatientChapter06/2.png)
