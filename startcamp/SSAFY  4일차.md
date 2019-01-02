### SSAFY  4일차



### 포멧팅

```python
"asdf{}".format(a)
== f"asdf{a}"
```

1) https://api.telegram.org/bot<token>/setWebhook?url=<url+/token>

-> https://api.telegram.org/bot<토큰>/setWebhook?url=https://python-dongsik93.c9users.io/<토큰>



2) https://api.telegram.org/bot<토큰>/getWebhookinfo    //웹훅을 이 주소로 설정했다라는 의미





### 네이버 개발자 사이트

https://developers.naver.com/



heroku 업로드

git add .

git commit -m ""

git push heroku master 

헤로쿠에 데이터 전송

sw 추천사이트!



### 배포

```python
동식님꺼 참조
heroku login

touch runtime.txt // 생성후 열기

python-3.6.7  // 입력

touch Procfile // 생성 후 열기

web: python app.py // 입력 (띄어쓰기 중요)

touch requirements.txt 

pip freeze > requirements.txt    // 서버에 pip설치했다는걸 서버에 알려줌

git add .

git commit -m " "

heroku create <자신이 만들 특별한 id>

git push herok master

```

 https://dubiduba-chatbot.herokuapp.com/ deployed to Heroku 이거  url 누르기

새로운 챗봇 하나 만들기 (토큰2)

https://api.telegram.org/bot<토큰2>/setWebhook?url=https://dubiduba-chatbot.herokuapp.com/<토큰2>

헤로쿠 들어가서 새로고침

들어가서 -> settings -> reveal config vars클릭

들어가서   TELE_TOKEN <토큰2> 넣어주면 됨

네이버 id

네이버 id secret 



소프트웨어 공부 하는 사이트

https://swexpertacademy.com/main/main.do

챗봇 개발

```python
챗봇 개발
```





