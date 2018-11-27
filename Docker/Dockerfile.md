# Dockerfile

* Docker image를 생성하기 위한 file

* **<명령> <매개 변수>**

* 작성된 명령을 순서대로 처리

* 명령은 항상 **FROM**으로 시작!

* 각 명령은 독립적

* 이미지를 생성할 때는 Dockerfile이 있는 디렉터리에서 **docker build**

* Docker Hub에 이미지를 올리려면 **<사용자명>/<이미지 이름>**

* **--tag** or **-t** 옵션으로 이미지 이름 설정

  ```shell
  $ sudo docker build --tag example .
  $ sudo docker build --tage pyrasis/example .
  ```


### [.dockerignore]

* Docker deamon에 필요없는 파일을 제외하려면 **.dockerignore** (.gitignore처럼!)

### [FROM]

* 어떤 이미지를 기반으로 이미지를 생성할지 설정
* **FROM <image name>**: latest로 자동 설정됨
* **FROM <image name>:<tag>**
* FROM에 설정한 이미지가 로컬에 있으면 바로 사용, 없으면 Docker Hub에서 받아옴
* FROM 여러 개 설정 가능:  두개 설정하면 두 개 생성, 
* 이 경우, **--tag**옵션으로 이미지 이름을 지정하면 마지막 이미지에 적용됨



### [MAINTAINER]

* 이미지를 생성한 사람의 정보

* 보통 이름과 이메일을 쓴다

  MAINTAINER Beee, <hell@gmail.com>

* 생략 가능!



### [RUN]

* FROM에서 설정한 이미지 위에서 스크립트 or 명령 실행
* 이 실행 결과가 이미지로 생성
* 실행 내용들은 이미지 히스토리에 기록됨
* **RUN <명령>**



### [CMD]

* 컨테이너가 시작되었을 떄 스크립트 or 명령 실행
* **docker run**이나 **docker start** 이 후 시작
* Dockerfile에서 한 번만 사용 가능
* 만약 Dockerfile에 **ENTRYPOINT**를 설정한다면 CMD는 ENTRYPOINT에 매개 변수 전달 역할 > 독자적으로 파일 실행X
* 만약 **docker run <이미지> <실행 파일>**에서 **실행파일**을 설정하면 CMD는 무시됨  
* 실행파일과 같은 기능임



### [ENTRYPOINT]

- 컨테이너가 시작되었을 떄 스크립트 or 명령 실행
- **docker run**이나 **docker start** 이 후 시작
- Dockerfile에서 한 번만 사용 가능
- **CMD**와 docker run 명령에서 동작방식이 다름
-  **docker run <이미지> <실행 파일>**에서 **실행파일**을 설정하면 실행 파일 설정을 매개 변수로 받아서 처리



### [EXPOSE]

* 호스트와 연결할 포트 번호 설정
* docker run의 **--expose**옵션과 동일



### [ENV]

* 환경 변수설정
* RUN, CMD, ENTRYPOINT에 적용
* **ENV <환경 변수> <값>**



### [ADD]

* 파일을 이미지에 추가
* **ADD <복사할 파일 경로> <이미지에서 파일이 위치할 경로>**
* **<복사할 파일 경로>**
  * 컨텍스트 아래를 기준! 컨텍스트 밖 절대 사용 불가!
  * 디렉터리 지정 가능! 아래 모든 파일까지 복사
  * *을 사용하여 특정 파일만 복사 가능
  * ex. ADD *.txt /root/
  * 인터넷에 있는 파일의 URL 설정 가능
* **<이미지에서 파일이 위치할 경로>**
  * 항상 절대 경로로 설정!
  * .dockerignore 파일에 설정된 파일은 복사 안됨

* 로컬에 있는 압축 파일은 압축을 해제하고 tar 풀어서 추가
* 인터넷에 있는 파일은 tar 해제 X > RUN으로 curl로 파일을 받은 뒤 압축 해제

### [COPY]

* 파일을 이미지에 추가
* 압축 파일은 압축 해제 안해줌
* 파일 URL 사용불가

- **ADD <복사할 파일 경로> <이미지에서 파일이 위치할 경로>**
- **<복사할 파일 경로>**
  - 컨텍스트 아래를 기준! 컨텍스트 밖 절대 사용 불가!
  - 디렉터리 지정 가능! 아래 모든 파일까지 복사
  - *을 사용하여 특정 파일만 복사 가능
  - ex. ADD *.txt /root/
  - 인터넷에 있는 파일의 URL 사용 불가

* **<이미지에서 파일이 위치할 경로>**
  * 항상 절대 경로로 설정!
  * .dockerignore 파일에 설정된 파일은 복사 안됨



### [VOLUME]

* 디렉터리의 내용을 컨테이너에 저장 X, Host에 저장
* **VOLUME <컨테이너 디렉터리>** or **VOLUME ["컨테이너 디렉터리1", "컨테이너 디렉터리2"]**

* Host의 특정 디렉터리와 연결하려면

  **-v <호스트 디렉터리>:<컨테이너 디렉터리>**



### [USER]

* 사용자 계정 설정
* USER 뒤에오는 RUN, CMD, ENTRYPOINT에 적용
* 중간에 바꾸면 그 밑으로는 바꾼 USER로 적용
* **USER <계정 사용자명>**



### [WORKDIR]

* RUN, CMD, ENTRYPOINT의 명령이 실행될 디렉터리 설정
* **WORKDIR <경로>**
* WORKDIR 뒤에 오는 모든 RUN, CMD, ENTRYPOINT에 적용
* 중간에 바꾸면 그 밑으로는 바꾼 WORKDIR 적용
* 절대경로, 상대 경로 다 사용가능
* BUT! 상대경로를 먼저쓰면 뒤에서 WORKDIR가 바껴도 상대경로를 기준으로 바꿈 > 최초는 /



### [ONBUILD]

* 생성된 이미지를 기반으로 다른 이미지가 생성될 때 명령을 trigger
* 즉, 다음 번 이미지에 FROM으로 사용될 때 실행할 명령 예약
* **ONBUILD <Dockerfile 명령> <Dockerfile 명령의 매개 변수>**
* FROM, MAINTAINER, ONBUILD를 제외한 모든 Dockerfile  명령어 사용 가능

* 손자 이미지에는 적용 X



# THE END

