### Github Blog 개설하기

# 1. Github Repository 개설

* Repositoy를 개설할 때, Repository name을 "**{Owner name}.github.io**"로 설정한다.

![1542111863499](C:\Users\Beee_\AppData\Roaming\Typora\typora-user-images\1542111863499.png)

* 이제 내가 blog 글을 저장할 dir로 가서 clone을 하면 된다.

  ```
  git clone https://github.com/JJOY07/JJOY07.github.io.git
  ```



# 2. Ruby 설치 (Ubuntu)

github 블로그 테마를 이용할 때는 jekyll을 설치해야하는데, 

이 전에 루비를 먼저 설치해야 한다.



* apt-get update 및 각종 디펜던시 설치

```
$ sudo apt-get update 
$ sudo apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev nodejs
```

* rbenv 가상환경 설치 (프로그래밍 언어 버전 관리)

  ```
  $ git clone https://github.com/rbenv/rbenv.git ~/.rbenv 
  $ echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc 
  $ echo 'eval "$(rbenv init -)"' >> ~/.bashrc 
  $ exec $SHELL
  ```

* ruby-build 설치

  ```
  $ git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build 
  $ echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc 
  $ exec $SHELL
  ```

* rbenv를 이용해 ruby 설치

  ```
  $ rbenv install 2.4.4 
  $ rbenv global 2.4.4 
  $ rbenv rehash
  ```

* Ruby 버전 확인

  ```
  $ ruby -v
  ```

* Ruby에서 사용하는 패키지인 Gem의 의존성관리 도구 bundle 설치

  ```
  $ gem install bundler
  $ rbenv rehash
  ```



# 3. Jekyll 설치

```
$ sudo gem install jekyll
```

[지킬 테마 모음 사이트](http://jekyllthemes.org)에서 원하는 테마를 다운 받고 commit하면 내 블로그에 테마가 적용이 된다.

(블로그는 {Owner name}.github.io 로 접속할 수 있다.)



이제 선택한 Jekyll 테마를 커스텀해서 사용하면 되는데,

이 부분은 다음 시간에 계속해 보자!