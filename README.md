# 물고기 도감 프로젝트

## 이미지 크롤링 하기(Window 기준)
---

+ 이미지 크롤링 하기에 앞서 필요 라이브러리를 다운 받습니다.

```
pip3 install selenium
pip3 install bs4
```
+ 이후 chromedriver.chromium.org/downloads 에 접속해 크롬 브라우저 버전에 맞는 크롬 드라이버를 설치해주세요(설치 폴더는 c:에 해주세요. 기본적으로 소스코드가 c:로 설정되어있습니다)
+ 크롬 브라우저 버전은 chrome://version에서 확인 할 수 있습니다.


+ 설치가 완료되고 나면 에디터로 crawl.py를 열어, dataset을 어디다 받을지 정해주세요
+ 기본 설정 폴더는 c:/crawling/ 입니다

+ 이제 크롤링을 시작합니다. 아래의 파일을 실행하면, 검색 키워드와 몇 장 크롤링 할 것인지에 대해 입력을 해주세요. 그럼 크롤링이 시작됩니다.

```
python3 crawl.py
```
---

