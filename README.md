[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![Apache-2.0 License][license-shield]][license-url]
<!-- [![license](https://img.shields.io/github/license/:user/:repo.svg)](LICENSE) -->

<p align="center">
  <a href="https://github.com/warumono-for-develop/jupyter-notebook-installation-tutorial">
    <img src="https://github.com/warumono-for-develop/default/blob/master/logos/warumono-logo-492x500.png?raw=true" alt="Logo" width="292" height="300">
  </a>

  <h1 align="center">Jupyter Notebook Installation Tutorial</h1>

  <p align="center">
    AWS EC2 인스턴스 접속 및 리소스 관리, CLI 등을 웹 브라우져를 이용하여 관리 하는 Jupyter Notebook 프로그램 설치 관련 지침서
    <br />
    <a href="https://github.com/warumono-for-develop/jupyter-notebook-installation-tutorial"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/warumono-for-develop/jupyter-notebook-installation-tutorial">View Tutorial</a>
    ·
    <a href="https://github.com/warumono-for-develop/jupyter-notebook-installation-tutorial/issues">Report Bug</a>
    ·
    <a href="https://github.com/warumono-for-develop/jupyter-notebook-installation-tutorial/issues">Request Feature</a>
  </p>
</p>

## Table of Contents 목차

- [Getting Started](#getting-started)
- [Install](#install)
- [Usage](#usage)
- [API](#api)
- [FAQ](#faq)
- [Contributing](#contributing)
- [Contact](#contact)
- [License](#license)

## Getting Started 시작하기

<kbd>⌥</kbd>    
<kbd>⌃</kbd>    
<kbd>⇧</kbd>    
<kbd>⌫</kbd>    
<kbd>⌦</kbd>    
<kbd>⌘</kbd>    

<details> 
  <summary>Collapse</summary>
  Expanded
</details>

### Requirements 요구사항

본 작업에 앞서 관련 대상 프로그램, 데이터 및 서버 등은 반드시 백업 완료 후 작업할 것을 권장   
본 작업을 작업하는 시점, 프로그램 버전 및 환경 등이 달라 설명 글의 진행 절차 또는 결과가 다소 다르거나 생략 또는 추가 작업이 있을 수 있음    
잘못된 용어 또는 정보가 다분히 포함되어 있는 비전문 지식을 바탕으로 설명되어 있으므로 공식 사이트 등에서 관련 정보를 미리 숙지하고 작업할 것을 권장

### About The Tutorial 지침서에 대하여

  - AWS EC2 를 사용한다면, EC2 내부의 리소스 관리는 물론 [CLI](https://namu.wiki/w/CLI) 이용 등은 필수적인 작업 중 일부   
  - 번거롭고 반복적인 작업으로 인해 효율성이 떨어지는 문제를 조금이나마 해소하고자 설치   
  - 보다 나은 작업환경을 만들어 보겠다고 생소한 용어들과 이해할 수 없는 원리 그리고 설정 등으로 인해 몇 차례 포기한 경험이 있지만    
이번에야말로 완료 해보겠다는 생각으로 여러번의 실패 끝에 나름 성공한 결과를 토대로 설정 정보 및 진행순서 등을 기록한 지침서

### Prerequisites 전제조건

#### Required 필수사항

  - [x] [AWS](https://aws.amazon.com/ko/) EC2 Instance    
    \[Free tier\] Ubuntu Server 18.04 LTS (HVM), SSD Volume Type

  - [x] [Python](https://www.python.org/)   
    Python 3.6.9    
    *Ubuntu Server 18.04 LTS 에 기본적으로 설치되어 있음*
  
#### Optional 선택사항

  - [ ] [OpenSSL](https://www.openssl.org/)   
    OpenSSL 1.1.1  11 Sep 2018    
    *Ubuntu Server 18.04 LTS 에 기본적으로 설치되어 있음*

## Install 설치

This module depends upon a knowledge of [Markdown]().

### Step 1

Install python3-pip

> apt-get update    
> apt-get install python3-pip

```sh
your-terminal> sudo apt-get update
...
your-terminal> sudo apt-get install python3-pip
...
```

### Step 2

Install Jupyter Notebook

> pip3 install notebook

```sh
your-terminal> sudo pip3 install notebook
...
```
### Step 3

Generate password for Jupyter Notebook

사용자가 입력한 비밀번호를 자동변환하여 나온 해시 값은 **메모하여 이 후 설정 단계에서 사용**   
작업 완료 후, <kbd>control</kbd> + <kbd>Z</kbd> 또는 <kbd>control</kbd> + <kbd>D</kbd> 키 입력으로 python3 에서 나옴

> python3   
> from notebook.auth import passwd    
> passwd()

> 'sha1:\<generated-your-password-hash-value\>'

```sh
your-terminal> python3
Python 3.6.5 ...
.....
>> from notebook.auth import passwd
>> passwd()
Enter password:
Verify password:
'sha1:g0bf6y023f60:75h6h014f68d70c03175et61p4675c497b83u63'
```

### Step 4

Configure Jupyter Notebook

설정 파일을 생성하고 vim 에디터를 이용하여 비밀번호 등의 정보를 입력
*설정 파일은 Jupyter Notebook 기본 설정 정보가 포함되어 생성 됨*

> jupyter notebook --generate-config
> vi ~/.jupyter/jupyter_notebook_config.py

```sh
your-terminal> jupyter notebook --generate-config
Writing default config to: /home/ubuntu/.jupyter/jupyter_notebook_config.py
your-terminal> sudo vi ~/.jupyter/jupyter_notebook_config.py
```

<details> 
  <summary>[Optional] SSL 사설 인증서 생성</summary>
SSL 을 사용하지 않아도 Jupyter Notebook 을 사용하는데 문제는 없으나 보안성을 높이기 위하여 사용하는 것을 권장   
사설 인증서보다는 정상적인 인증기관으로부터 발급받은 인증서를 사용할 것을 권장

> sudo openssl req -x509 -nodes -days {valid-days} -newkey rsa:1024 -keyout "{your-juypter-notebook-ssl-keyfile-name}.key" -out "{your-jupyter-notebook-ssl-certfile-name}.pem" -batch

```sh
your-terminal> mkdir ~/{your-ssl-file-directory-name}
your-terminal> cd {your-ssl-file-directory-name}
your-terminal> sudo openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout "my-jupyter-notebook-key.key" -out "my-jupyter-notebook-cert.pem" -batch
your-terminal> ls
my-jupyter-notebook-key.key  my-jupyter-notebook-cert.pem
```

---
</details>

설정 파일 기존 내용의 마지막 아래에 설정 내용 추가 입력

> c = get_config()    
> c.NotebookApp.password = u'{generated-your-password-hash-value}'    
> c.NotebookApp.ip = '{your-host-ip | your-aws-ec2-private-ips}'    
> c.NotebookApp.notebook_dir = '{your-host-begin-path}'   
> c.NotebookApp.keyfile = u'{your-juypter-notebook-ssl-keyfile-name}.key'   
> c.NotebookApp.certfile = u'{your-jupyter-notebook-ssl-certfile-name}.pem'

```sh
...
# ============================================================
# my jyputer-notebook configuration
# ============================================================
c = get_config()
c.NotebookApp.password = u'sha1:g0bf6y023f60:75h6h014f68d70c03175et61p4675c497b83u63'
c.NotebookApp.ip = '172.31.35.203'
c.NotebookApp.notebook_dir = '/home/ubuntu'
```

<details> 
  <summary>[Optional] SSL 사설 인증서 적용</summary>
SSL 을 적용하고자 사설 인증서를 생성하였다면, 다음 설정 내용을 추가로 입력

> c.NotebookApp.keyfile = u'{your-juypter-notebook-ssl-keyfile-name}.key'
> c.NotebookApp.certfile = u'{your-jupyter-notebook-ssl-certfile-name}.pem'

```sh

c.NotebookApp.keyfile = u'my-jupyter-notebook-key.key'
c.NotebookApp.certfile = u'my-jupyter-notebook-cert.pem'
```

---
</details>

### Step 5

Jupyter Notebook 백그라운드 실행 설정

정상적으로 Jupyter Notebook 의 설치 및 설정이 완료된 후 터미널을 이용하여 실행하고, 해당 터미널을 닫거나 임의로 끊기는 경우에는 Jupyter Notebook 프로그램도 중지가 되므로 이를 방지하기 위하여 백그라운드에서 실행되도록 설정할 것을 권장

> bg
> disown -h

```sh
your-terminal> bg
[3]+ sudo jupyter-notebook --allow-root &
your-terminal> disown -h
```

## Usage 사용방법

정상적으로 Jupyter Notebook 설치 및 설정이 완료되었다면 실행하여 웹 브라우져로 접근 후 확인

### Run Jupyter Notebook

> jupyter-notebook --allow-root
> ...
> [...] https://{your-host-ip | your-aws-ec2-private-ips}:{your-jupyter-notebook-port}/
> ...

```sh
your-terminal> sudo jupyter-notebook --allow-root
...
[...] https://172.31.35.203:8888/
...
```

### Connect to Jupyter Notebook with Web Browser

웹 브라우져를 실행하고 URL 입력 창에 [**`https://{your-host-ip | your-aws-ec2-private-ips}:{your-jupyter-notebook-port}/`**](#run-jupyter-notebook) 를 입력하여 접속    
Google Chrome 브라우져의 경우, 알 수 없는 인증기관에서 발급된 사설인증서를 이용한 사이트 접근을 우선적으로 방지하고 있어 `경고 화면`이 나오게 됨   
이 경우, 경고 화면에서 어떠한 동작도 하지 않고 **`thisisunsafe`** 문자를 키보드로 입력하면 Jupyter Notebook Dashboard 화면으로 접근 가능

### Jupyter Notebook Dashboard

*Jupyter 공식 웹사이트의 예시 화면*    
예시 화면의 오른쪽 위 **_`New`_** 버튼을 눌러 Drop Down 메뉴 중 **_`Terminal`_** 을 선택하면 새 브라우져 창(또는 새 탭)으로 터미널 화면이 나옴    
![Jupyter Notebook Dashboard](https://jupyter.readthedocs.io/en/latest/_images/tryjupyter_file.png)


### Jenkins

#### Configure 설정

  - [CloudBees Docker Hub/Registry Notification 2.4.0](https://plugins.jenkins.io/dockerhub-notification/) Plugin 설치    
  `Jenkins` &nbsp; > &nbsp; `Manage Jenkins` &nbsp; > &nbsp; `Manage Plugins` 화면    
  검색 입력 창에 `CloudBees` 입력 조회    
  `CloudBees Docker Hub/Registry Notification` 선택 설치 후, Jenkins 재가동   

  - Build Trigger & Build Execute shell 설정    
  Jenkins &nbsp; > &nbsp; \<your-job-name\> &nbsp; > &nbsp; Project <your-job-name> > Configure 화면    
  Build Trigger   
  - [ ] GitHub hook trigger for GITScm polling 항목 체크박스 비활성화(해제) : 사용자가 GitHub 으로 push 하는 것을 Webhook
  - [x] Monitor Docker Hub/Registry for image changes 항목 체크박스 활성화 : Docker Hub 에서 이미지 생성 또는 변경되는 것을 Webhook
  - [x] Specified repositories will trigger this job 항목 체크박스 활성화 : Webhook 된 사항에 따라 Jenkins 가 자동으로 임의의 작업 실행    
  Repositories 입력 창 {your-docker-image-name} 입력   
  Build Execute shell   
  ```sh
  # 기존 {your-docker-container-name} 컨테이너 삭제   
  # 단, 최초 실행(docker run)시 {your-docker-container-name} 컨테이너는 존재하지 않아 빌드가 실패하는 것을 방지하기 위하여 || true 구문을 넣어 정상적으로 진행 되도록 처리
  docker rm -f {your-docker-container-name} || true   
  docker pull {your-docker-image-name}    
  docker run -d -p {your-host-port}:{your-application-port} --name {your-docker-container-name} {your-docker-image-name}
  ```
  
  ```sh
  docker rm -f spring-boot-restful-api-server-repository || true
  docker pull warumono/spring-boot-restful-api-server
  docker run -d -p 8080:8080 --name spring-boot-restful-api-server-repository warumono/spring-boot-restful-api-server
  ```



```
```

Note: The `license` badge image link at the top of this file should be updated with the correct `:user` and `:repo`.

### Any optional sections

## FAQ

<details> 
  <summary>User variable 사용자 변수</summary>
본 지침서는 작성자의 기준으로 설명하다보니 모든 작업의 내용대로 복사하여 사용할 경우 의도하지 않은 과정이나 결과를 도래할 수 있기에,
사용자 자신의 환경에 맞추거나 또는 원하는 내용대로 작업할 수 있도록 설명하기 위하여 변수 형태로 사용    


- `{variable-name}` 사용자가 직접 입력해야하는 부분. http://`{your-host-ip}`:8080 &nbsp; - - - > &nbsp; http://`123.456.789.0`:8080    
- `<variable-name>` 사용자의 어떠한 행위에 따른 제공되는 결과 부분. `<your-cert-key-name>`.pem &nbsp; - - - > &nbsp; `my_cert`.pem

---
</details>

<details> 
  <summary>VIM 에디터 간단 사용 방법</summary>
본 지침서는 Linux 계열의 OS 기준으로 설명하다보니 VIM 에디터의 vi 명령어로 파일 내용을 편집하는 경우가 빈번하여 간단하게 설명   
사용자 자신의 환경과 맞지 않을 경우에는 프로그램 설치 등으로 이에 준하는 환경에서 작업할 것을 권장


### VIM 에디터 실행

vi 명령어 이용

> vi {your-file-name}

```sh
your-terminal> vi README.md
```

이 파일명의 파일이 존재하면 해당 파일을 열어서 보여주고 (아직 읽기만 가능한 상태) "{your-file-name}" file info aaa
존재하지 않을 경우 해당 파일명과 동일한 이름을 갖는 새 파일을 열음 (아직은 저장되지않은상태 ) "{your-file-name}" [New File]
이 상태에서 i또는 a또는 o를 누르면 ex 명령 부분
내용 편집 후 <kbd>esc</kbd> 를 누르면 ex 명령 모드 전환 (아직은 저장되지 않은 상태).


#### 명령 모드 
*파일 내용 읽기만 가능*한 상태
커서의 이동, 수정, 삭제, 복사, 붙여넣기 그리고 탐색 등의 기능 수행
<kbd>i</kbd>, <kbd>a</kbd>, <kbd>o</kbd>, <kbd>I</kbd>, <kbd>A</kbd>, <kbd>O</kbd> 등의 키를 눌러서 입력 모드로 전환
입력 모드 또는 ex 명령 모드 상태에서 <kbd>esc</kbd> 키를 누르면 명령 모드로 전환

#### 입력 모드 | 편집 모드 | input mode | insert mode
*파일 내용 편집이 가능*한 상태    
명령 모드에서 입력 전환키를 누르면 에디터의 왼쪽 아래 모서리 부분에 `-- INSERT --` 로 전환되었음을 알려주고 <kbd>esc</kbd> 키를 누르면 `-- INSERT --` 가 사라지므로써 입력 모드에서 명령 모드로 전환됨
자주 사용되는 명령어는 다음 표와 같으며 대부분 화면에 입력한 키가 나타나지는 않으므로 현재 모드를 확인하며 작업

|명령어 \| 키|설명|비고|
|---:|---|---|
|<kbd>x</kbd>|현재 커서가 위치한 문자 삭제|<kbd>del</kbd> 키 기능|
|<kbd>dw</kbd>|단어 삭제||
|<kbd>dd</kbd>|현재 커서가 위차한 행 삭제||
|{숫자} + <kbd>dd</kbd>|현재 커서가 위치한 행부터 숫자만큼의 행 삭제||
|<kbd>yy</kbd>|현재 커서가 위치한 행 복사||
|{숫자} + <kbd>yy</kbd>|현재 커서가 위치한 행부터 숫자만큼의 행 복사||
|<kbd>p</kbd>|복사한 내용을 현재 커서가 위치한 행 이후 행에 붙여 넣기||
|<kbd>P</kbd>|복사한 내용을 현재 커서가 위치한 행 이전 행에 붙여 넣기|<kbd>⇧</kbd> + <kbd>p</kbd> 와 동일|
|<kbd>u</kbd>|직전 실행한 명령 취소|undo|
|<kbd>/exp</kbd> + <kbd>enter</kbd>|'exp' 문자열을 현재 커서 위치에서 오른쪽 또는 아래 방향에서 검색||
|<kbd>n</kbd>|찾은 문자가 여러개인 경우 현재 커서 위치에서 오른쪽 또는 아래 방향으로 일치하는 다음 문자 위치로 이동||
|<kbd>N</kbd>|찾은 문자가 여러개인 경우 현재 커서 위치에서 왼쪽 또는 위 방향으로 일치하는 이전 문자 위치로 이동|<kbd>shift</kbd> + <kbd>n</kbd> 와 동일|

### ex 명령 모드 | 라인 명령 모드
명령 모드 상태에서 입력하는 키가 `에디터의 왼쪽 아래 모서리 부분`에 나타나며 ex 명령어를 이용하여 *에디터 저장, 종료, 탐색, 치환 및 vi 환경 설정 등이 가능*한 상태
명령 모드에서 <kbd>:</kbd> 키 입력으로 시작

|명령어 \| 키|설명|비고|
|---:|---|---|
|<kbd>q</kbd>|편집기 종료||
|<kbd>w</kbd>|저장||
|<kbd>!</kbd>|강제실행||

```
:q
```
편집한 내용이 있다면 저장하지 않은 것에 에러를 보여주며 편집기는 종료되지 않음

```
:q!
```
편집한 내용은 저장하지 않고 편집기 종료

```
:wq
```
편집한 내용은 저장하고 편집기 종료

### VIM 에디터 줄 번호 보기

지정된 파일 이름으로 생성하여 명령어 한 줄 입력 후 저장하는 것만으로 설정 가능

> vi ~/.vimrc

```sh
your-terminal> vi ~/.vimrc
```

.vimrc 파일에 명령어 한 줄 입력 후 저장

> set number

```sh
set number
```
* 또한, 파일 내용 보기 명령어 `cat` 은 옵션 `-n` 을 이용하여 줄 번호 보기 가능

> cat -n {your-file-name}

```sh
your-terminal> cat -n .vimrc
     1  set number
```

---
</details>

## More optional sections

## Contributing

See [the contributing file](CONTRIBUTING.md)!

PRs accepted.

Small note: If editing the Readme, please conform to the [standard-readme](https://github.com/RichardLitt/standard-readme) specification.

### Any optional sections

## Contact

### Any optional sections

## License

[MIT © Richard McRichface.](../LICENSE)

<!-- MARKDOWN LINKS & IMAGES -->

<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->

[spring-boot-restful-api-server-template]: https://github.com/warumono-for-develop/spring-boot-restful-api-server-template "Spring Boot RESTFul API Server Template"
[docker-installation-tutorial]: https://github.com/warumono-for-develop/docker-installation-tutorial "Docker Installation Tutorial"
[jenkins-installation-tutorial]: https://github.com/warumono-for-develop/jenkins-installation-tutorial "Jenkins Installation Tutorial"
[jupyter-notebook-installation-tutorial]: https://github.com/warumono-for-develop/jupyter-notebook-installation-tutorial "Jupyter Notebook Installation Tutorial"

[contributors-shield]: https://img.shields.io/github/contributors/warumono-for-develop/jenkins-installation-tutorial.svg?style=flat-square
[contributors-url]: https://github.com/warumono-for-develop/jenkins-installation-tutorial/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/warumono-for-develop/jenkins-installation-tutorial.svg?style=flat-square
[forks-url]: https://github.com/warumono-for-develop/jenkins-installation-tutorial/network/members
[stars-shield]: https://img.shields.io/github/stars/warumono-for-develop/jenkins-installation-tutorial.svg?style=flat-square
[stars-url]: https://github.com/warumono-for-develop/jenkins-installation-tutorial/stargazers
[issues-shield]: https://img.shields.io/github/issues/warumono-for-develop/jenkins-installation-tutorial.svg?style=flat-square
[issues-url]: https://github.com/warumono-for-develop/jenkins-installation-tutorial/issues
[license-shield]: https://img.shields.io/github/license/warumono-for-develop/jenkins-installation-tutorial.svg?style=flat-square
[license-url]: https://github.com/warumono-for-develop/jenkins-installation-tutorial/blob/master/LICENSE
[product-screenshot]: images/screenshot.png
