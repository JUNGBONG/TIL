## SSAFY 3일차

```python
from flask import Flask, render_template
import random

app = Flask(__name__)

@app.route("/")
def hello():
    return "<h1>서버가 html도 보내주나???</h1>"
    
@app.route("/html_tag")
def html_tag():
    return """
    <h1>첫번째 줄!!!</h1>
    <h2>두번째 줄!!</h2>
    """

@app.route("/html_file")
def html_file():
    return render_template("html_file.html")
    
@app.route("/welcome/<string:name>")
def welcome(name):
    return render_template("welcome.html", people=name)
    
@app.route("/cube/<int:num>")
def cube(num):
    triple = num*num*num
    return render_template("cube.html",triple=triple,num=num)
    
@app.route('/lunch')
def lunch():
    # 요부분에 점심메뉴를 추천해주는 코드를 작성!
    menu_list = ["삼겹살","피자","치킨"]
    pick = random.choice(menu_list)
    return render_template("lunch.html",pick=pick)

@app.route('/lotto')    
def lotto():
    numbers = range(1,46)
    pick = random.sample(numbers,6)
    sort_pick = sorted(pick)
    return render_template("lotto.html",sort_pick=sort_pick)

@app.route('/naver')
def naver():
    return render_template("naver.html")
    
@app.route('/google')

```



<!--html안에서 파이썬 코드를 쓰려면 {##}를 쓰자-->

```python
>>> print(123)
123
>>> type(123)
<class 'int'>
>>> type("123")
<class 'str'>
>>> type([])
<class 'list'>
>>> type({})
<class 'dict'>
>>> type(True)
<class 'bool'>
```

## 오전은 로또

```python
from flask import Flask, render_template
import random
import requests
import json
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"
    
    
@app.route('/lotto')
def lotto():
    url = "https://www.dhlottery.co.kr/common.do?method=getLottoNumber&drwNo=837"
    res = requests.get(url).text
    lotto_dict = json.loads(res)
    print(lotto_dict["drwNoDate"])
    
    
    week_num = []
    week_format_num = []
    drwtNo = ["drwtNo1","drwtNo2","drwtNo3","drwtNo4","drwtNo5","drwtNo6"]
    for num in drwtNo:
        number =lotto_dict[num]
        week_num.append(number)
        print(week_num)
    #포멧팅 "a{}".format(b)
     
    # for i in range(1,7):
    #      week_format_num.append(lotto_dict["drwtNo{}".format(i)])
    for i in range(1,7):
        num = lotto_dict["drwtNo{}".format(i)]
        week_format_num.append(num)
        
    num_list = range(1,46)
    pick = random.sample(num_list,6)
        
    #pick =우리가 생성한 번호
    #week.num =이번주 당첨번호
    ###### 위의 두 값을 비교해서 로또 당첨 등수 출력!!!!
    #sorted()
    #1등 :6개의 숫자를 다 맞출때
    #2등 :5개의 숫자 + 보너스 번호
    #3등 :5개의 숫자
    #4등 :4개의 숫자
    #5등 :3개
    #꽝
         
    count = 0
    n = 0 
    count1 = 0
    pick =[2, 25, 28, 30, 33, 6]
    while n < 6:
        for j in range(6):
            if pick[j] == week_format_num[n]:
                count = count+1
            # elif bnusNo == week_format_num[jn]:
                # count1 = count1 +1
        n= n+1 
   
    if count == 6:
        print("1등입니다.")
    elif count ==5and count1 ==1 :
        print("2등입니다.")
        
    elif count ==5:
        print("3등입니다.")
    elif count ==4:
        print("4등입니다.")
    elif count ==3:
        print("5등입니다.")
    else:
        print("꽝입니다..")
           
    
    
    
    #대괄호로 호출
    # print(type(res))
    # print(type(json.loads(res)))
    
    
    return render_template("lotto.html",lotto=pick, week_num=week_num, week_format_num=week_format_num)
   
'''@app.route('/lottery')
def lottery():
    #로또 정보를 가져온다. & 필요한것만 고른다.
    url = "https://www.dhlottery.co.kr/common.do?method=getLottoNumber&drwNo=837"
    res = requests.get(url).text
    lotto_dict = json.loads(res)
    #1등 당첨 번호를 week 리스트에 넣는다.
    week = []
    for i in range(1,7):
    num = lotto_dict['drwtNo{}'.format(i)]
    week.append(num)
    #보너스 번호를 bonus 변수에 넣는다.
    bonus = lotto_dict["bnusNo"]
    #임의의 로또 번호를 생성한다.
    pick = random.sample(range(1,46),6)
    #비교해서 몇등인지 저장한다.
     match = len(set(pick)&set(week))
    if match==6:
        text = "1등"
    elif match==5:
        if bonus in pick:
            text = "2등"
        else:
            text = "3등"
    elif match==4:
        text = "4등"
    else:
        text ="꽝"
        
    #사용자에게 데이터를 넘겨준다.
    
    return render_template("lottery.html",pick=pick,week=week,text=text)'''
```



### lotto.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <h1>여기는 로또 검증페이지 입니다.</h1>
    <!--html안에서 파이썬 코드를 쓰려면 {##}를 쓰자-->
    <h4>생성된 번호 : {{lotto}}</h4>
    <h5>이번주 번호 :{{week_num}}</h5>
</body>
</html>
```



### lottery.html

```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <h1>이번주 번호 : {{week}}</h1>
    <h1>생성된 번호 : {{pick}}</h1>
    <h1>너의 등수 :{{text}}</h1>
    
    
</body>
</html>
```



### ping.html

```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <form action ="/pong">
        <input type="text" name="name"/>
        <input type="submit" value="Submit"/>
    </form>
    
</body>
</html>
```





### ping.py

```python
from flask import Flask, render_template
import random
import requests
import json
import request
app = Flask(__name__)

@app.route('/ping')
def ping():
    return render_template("ping.html")

```

