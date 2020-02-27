<!-- SHIELDS -->
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]

<!-- LOGO -->
<br />
<p align="center">
  <a href="https://github.com/othneildrew/Best-README-Template">
    <img src="images/logo.png" alt="Logo" width="80" height="80">
  </a>

  <h1 align="center">Jupyter Notebook Installation Tutorial</h1>

  <p align="center">
    AWS EC2 인스턴스 접속 및 스토리지, 터미널을 웹 브라우져로 사용할 수 있는 Jypyter Notebook 설치에 관한 사용 지침서
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



<!-- TABLE OF CONTENTS -->
## Table of Contents

* [About the Tutorial](#about-the-tutorial)
  * [Official Website](#official-website)
  * [Built With](#built-with)
* [Getting Started](#getting-started)
  * [Prerequisites](#prerequisites)
  * [Installation](#installation)
* [Usage](#usage)
* [Roadmap](#roadmap)
* [Contributing](#contributing)
* [License](#license)
* [Contact](#contact)
* [Acknowledgements](#acknowledgements)



<!-- ABOUT THE PROJECT -->
## About The Tutorial

AWS EC2 인스턴스를 생성하였다면, 생성한 인스턴스에 접속하기 위하여 접속 관련 정보를 관리하고 사용해야하는데 있어 번거로움

터미널 프로그램을 이용하여 AWS EC2 인스턴스에 접속하고나서 터미널을 종료한다거나 일정시간이 지나면 접속이 자동으로 끊기는 경우에 재접속하고자 하는 경우 재차 접속 관련 정보를 입력해야하는 불편함

타인과 협업을 하게 될 경우, AWS 인증 키를 여러 개 만듦(또는 복사)으로써 관리하기에 불편하고 보안성이 떨어짐

Jupyter Notebook 을 사용하는 이유:
* EC2 접속 관련 정보 메모 불필요
* AWS 인증 키 관리 용이
* 파일 관리 및 구조 가독성 우수
* 로컬 운영체제와 별개로 타 운영체제 사용 가능

*물론 Jupyter Notebook 외 다른 좋은 방법들도 있으리라 생각하지만, 이 프로그램을 써보는 것도 추천*


### Official Website

공식 사이트 또는 관련 정보를 미리 숙지하고 사용할 것을 권장

* [Project Jupyter](https://jupyter.org/)


### Built with

[AWS](https://aws.amazon.com/ko/) EC2 Instance
<Free tier> Ubuntu Server 18.04 LTS (HVM), SSD Volume Type

[Python](https://www.python.org/)
Python 3.6.9
*Ubuntu Server 18.04 LTS 에 기본적으로 설치되어 있음*

[OpenSSL](https://www.openssl.org/)
OpenSSL 1.1.1  11 Sep 2018
*Ubuntu Server 18.04 LTS 에 기본적으로 설치되어 있음*

[Google Chrome Browser](https://www.google.com/intl/ko/chrome/)
Version 80.0.3987.122 (Official Build) (64-bit)



<!-- GETTING STARTED -->
## Getting Started

Jupyter Notebook 을 설치는 터미널을 이용하여 명령어를 입력하는 작업이 많으므로 진행 순서와 오탈자에 주의

*설명글에 나오는 용어 및 단어 등은 되도록 공식적(?)으로 사용되는 것으로 표기하였으나 오탈자 및 잘못된 용어 또는 정보가 있을 수 있음*

*your-teminal> 사용자의 터미널 프로그램 프롬프트를 나타내며 입력하는 문자가 아님*
*{your-xxx} : 사용자가 정의해야하는 항목 변수이며 임의의 이름이나 특정된 명칭 등으로 입력*


### Prerequisites

* AWS EC2 인스턴스 **생성** 및 **활성화**

* AWS EC2 인스턴스 내부 IP 정보

AWS EC2 인스턴스의 상세 정보 중 **Private IPs**

또한 이 정보는 터미널의 명령어를 이용하여 확인 가능
```sh
your-terminal> **ifconfig**
```

* AWS EC2 인스턴스의 보안 그룹 설정
AWS EC2 인스턴스에 적용되어 있는 보안 그룹으로 이동하여 Inbound 에 Jupyter Notebook 에 접속할 URL 의 PORT 추가

* OpenSSL 사설 인증서
*ssl 을 사용하지 않아도 Jupyter Notebook 을 사용하는데 문제는 없으나 사용하는 것을 권장*
```sh
your-terminal> cd ~
your-terminal> mkdir {your-ssh-file-directory-name}
your-terminal> cd {your-ssh-file-directory-name}
your-terminal> sudo openssl req -x509 -nodes -days {your-valid-date} -newkey rsa:1024 -keyout "{your-private-cert-file-name}.key" -out "{your-public-cert-file-name}.pem" -batch
your-terminal> ls
{your-private-cert-file-name}.key  {your-public-cert-file-name}.pem
```

### Installation

1. python3-pip 프로그램 설치
```sh
> sudo apt-get update
...

your-terminal> sudo apt-get install python3-pip
...
```

2. Jupyter Notebook 설치
```sh
your-terminal> sudo pip3 install notebook
...
```

3. Jupyter Notebook 비밀번호 설정

__정상적으로 입력한 비밀번호에 따른 해시 값이 나오면 이 해시 값을 메모하여 이 후 설정 단계에서 사용__

*비밀번호 설정 완료 후, **`control + Z`** 키를 눌러 python3 로 부터 나옴*
```sh
your-terminal> python3
Python 3.6.5 ...
.....
>> from from notebook.auth import passwd
>> passwd()
Enter password:
Verify password:
'sha1:a8dfhlqer234n239f7afdsa32470dfabdfl1234fj82m42jf9mnaaw8r'
```

4. Jupyter Notebook 설정파일 생성

*정상적으로 환경 설정 파일이 생성되면 해당 파일의 경로가 표시 됨*

*생성된 설정 파일에는 Jupyter Notebook 기본 설정 정보가 있음*
```sh
your-terminal> cd ~
your-terminal> jupyter notebook --geneate-config
Writing default config to: /home/ubuntu/.jupyter/jupyter_notebook_config.py
```

5. Jupyter Notebook 설정파일 편집
```sh
your-terminal> sudo vi ~/.jupyter/jupyter_notebook_config.py
```

jupyter_notebook_config.py 내용
```sh
...
# ============================================================
# your comment
# ============================================================
c = get_config()
c.NotebookApp.password = u'{your-jupyter-password-hash-value}'
c.NotebookApp.ip = '{your-aws-ec2-private-ip}'
c.NotebookApp.notebook_dir = '{your-jupyter-file-explorer-begin-path}'
c.NotebookApp.keyfile = u'{your-private-cert-file-name.key-full-path}'
c.NotebookApp.certfile = u'{your-public-cert-file-name.pem-full-path}'
```
6. Jupyter Notebook 백그라운드 실행 설정

정상적으로 Jupyter Notebook 의 설치 및 설정이 완료된 후 터미널을 이용하여 실행하고, 

해당 터미널을 닫거나 임의로 끊기는 경우에는 Jupyter Notebook 프로그램도 중지가 되므로 이를 방지하기 위하여 `백그라운드에서 실행되도록 설정`해야 함
```sh
your-terminal> bg
[3]+ sudo jupyter-notebook --allow-root &
your-terminal> disown -h
```



<!-- USAGE EXAMPLES -->
## Usage

정상적으로 Jupyter Notebook 설치와 설정이 완료되었다면, 실행하여 정상적으로 접근하여 사용할 수 있는지를 확인

* Jupyter Notebook 실행
```sh
your-terminal> sudo jupyter-notebook --allow-root
...
[...] https://{your-jupyter-notebook-url}:{your-jupyter-notebook-port}/
...
```

* Jupyter Notebook 접속

Google Chrome 브라우져를 실행하고 URL 입력 창에 `https://{your-jupyter-notebook-url}:{your-jupyter-notebook-port}/` 를 입력하여 접속

Google Chrome 브라우져의 경우 알 수 없는 인증기관에서 발급된 사설인증서를 이용한 사이트 접근을 우선적으로 방지하고 있어 `경고 화면`이 나오게 됨

이 경우, 경고 화면에서 어떠한 동작도 하지 않고 **`thisisunsafe`** 문자를 키보드로 입력하면 Jupyter Notebook 화면으로 접근 가능


<!-- ROADMAP -->
## Roadmap

See the [open issues](https://github.com/warumono-for-develop/jupyter-notebook-installation-tutorial/issues) for a list of proposed features (and known issues).



<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request



<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE` for more information.



<!-- CONTACT -->
## Contact

warumono - warumono.for.develop@gmail.com

Project link: [https://github.com/warumono-for-develop/jupyter-notebook-installation-tutorial](https://github.com/warumono-for-develop/jupyter-notebook-installation-tutorial)



<!-- ACKNOWLEDGEMENTS -->
## Acknowledgements
* [안경잡이개발자](https://ndb796.tistory.com/)
* [othneildrew](https://github.com/othneildrew)



<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/warumono-for-develop/jupyter-notebook-installation-tutorial.svg?style=flat-square
[contributors-url]: https://github.com/warumono-for-develop/jupyter-notebook-installation-tutorial/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/warumono-for-develop/jupyter-notebook-installation-tutorial.svg?style=flat-square
[forks-url]: https://github.com/warumono-for-develop/jupyter-notebook-installation-tutorial/network/members
[stars-shield]: https://img.shields.io/github/stars/warumono-for-develop/jupyter-notebook-installation-tutorial.svg?style=flat-square
[stars-url]: https://github.com/warumono-for-develop/jupyter-notebook-installation-tutorial/stargazers
[issues-shield]: https://img.shields.io/github/issues/warumono-for-develop/jupyter-notebook-installation-tutorial.svg?style=flat-square
[issues-url]: https://github.com/warumono-for-develop/jupyter-notebook-installation-tutorial/issues
[license-shield]: https://img.shields.io/github/license/warumono-for-develop/jupyter-notebook-installation-tutorial.svg?style=flat-square
[license-url]: https://github.com/warumono-for-develop/jupyter-notebook-installation-tutorial/blob/master/LICENSE.txt
[product-screenshot]: images/screenshot.png
