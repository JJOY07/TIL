# Docker Compose

* Docker Compose는 컨테이너를 이용한 서비스 개발과 CI(Continous Intergration)를 위하여 여러개의 컨테이너를 하나의 프로젝트로 다룰 수 있는 작업환경을 제공함



### 왜 필요한가?

웹 애플리케이션의 경우 필요한 컨테이너는?

- Web Server Container

- WAS Server Container

- DB Container

- 등등...

  > 개별 컨테이너 정상동작 확인 필요

##### 매번 CLI로 컨테이너를 생성할 것인가?

> 하나의 웹 애플리케이션(ex)를 위해 필요한 컨테이너를 하나로 관리면 엄청 편리할것!

##### 이 기능을 해주는게 바로 Docker Compose이다 :D

