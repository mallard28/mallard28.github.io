---
title: "Selenium Chrome driver 설정 자동으로 받아오기"
excerpt: "Selenium chrome driver 자동 설정"

categories:
    - Python
tags:
    - Python
    - Selenium
    - Webdriver
    - Chrome Web driver
    - Web Crawler
    - Web Scraping

toc: true
toc_sticky: true
---
## 1. ChromeDriver 다운로드
ChromeDriver는 Webdriver의 한 종류이다. WebDriver는 다양한 브라우저에서 webapp의 자동화 테스트를 위한 오픈소스 Tool이다. 웹페이지 이동, 사용자 입력,  JavaScript 실행 등의 기능을 제공하며, ChromeDriver는 안드로이드나 Mac, Linux, Windows 및 ChromeOS에서 동작하는 Chrome 웹브라우저를 위한 WebDriver이다.
<br><br>
ChromeDriver는 Chrome 브라우저를 사용한다고 해서 기본으로 포함되어 있는것은 아니며, 아래 경로를 통해 별도로 다운로드 받아야 사용이 가능하다.
<br><br>

> **[ChromeDriver Downloads](https://chromedriver.chromium.org/downloads)**

다운로드 받은 크롬 드라이버를 사용하기 위해서는 작업중인 폴더로 옮긴 후, 기본적으로 아래와 같이 사용한다.

```python
from selenium import webdriver

driver = webdriver.Chrome
```

## 2. ChromeDriver Version 이슈

ChromeDriver는 앞서 말한것처럼 webapp 자동화를 위해서 쓰이며, 주로 Python을 사용한 Web Scraping 기능을 구현할 때 필수적으로 쓰인다. 이때 Chrome 브라우저의 버전과 다운로드 받은 ChromeDriver의 버전이 호환성이 맞아야 프로그램이 제대로 동작하게 된다. 버전이 맞지않을 경우(충돌) 아예 실행이 불가능 하며, 해결하기 위해서는 Chrome 브라우저 또는 ChromeDriver중 어느 하나의 버전을 변경하여 다시 설치하거나 업데이트를 해야 한다.

문제는 바로 여기서 발생하게 된다. 보통 Web Scraping을 위해 웹크롤러를 개발하고, 일정 주기로 자료를 수집하도록 스케줄러나 배치에 등록하여 자료 수집을 진행하게 된다. 평소에는 문제없이 잘 동작하지만 Chrome 브라우저의 자동 업데이트 등과 같은 이유로 버전이 달라지거나 ChromeDriver의 설치 경로가 맞지 않을 경우 아무 동작도 하지 않게 되는 이슈가 발생하게 된다.


## 3. Code 구현
위 문제를 해결하기 위한 방법으로 실행시마다 현재 위치에 ChromeDriver를 설치하도록 아래와 같이 소스코드를 구현해 놓는다.
먼저 pip 명령어로 wevdriver-manager를 설치해준다.

```console
pip install webdriver-manager
```

설치가 끝나면 아래와 같이 webdriver 설정 코드를 넣어주고 기존 코드를 삭제한다.

```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager

def Auto_ChromeDriver():

    driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()))
```