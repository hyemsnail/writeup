# Space WAR #7 Write up 
인생 두번째 CTF에 참여해보았다. 이번에도 Web 분야로 참여해보았다. flagreading(?)이라는 이름으로 되있었고 무엇보다 난이도가 easy여서 이 분야로 해보게 되었다. 8일 전에 CTF를 참여해보았지만 아직도 아무것도 아는게 없는 상태이기 때문에 경험을 쌓는 것에 의의를 둘 것이다.

처음에 파일을 받으면 flag.txt, app.py, dockerfile, docker-compose.yml , index.html파일이 있다. index.html은 열면 Web Shell 이라는 이름으로 아래 사진같은 사이트가 뜬다. 

![스크린샷 2024-04-28 135351](https://github.com/hyemsnail/Space_WAR/assets/163375128/496d25d0-0216-4bb1-be3e-b076efa69563)

딱 봐도 Enter a shell command 안에 맞는 답을 집어넣으면 꽤 큰 진전이 있을 것 같다. 

flag.txt파일을 봤는데 모양새가 웬지 답 같이 생겨서 shell command와 flag에 한번 둘다 넣어보았다. 
![스크린샷 2024-04-28 150104](https://github.com/hyemsnail/Space_WAR/assets/163375128/f560d2ad-6416-4a2e-b5f4-9607d5c1228e)
![스크린샷 2024-04-28 135311](https://github.com/hyemsnail/Space_WAR/assets/163375128/67b07896-b783-49ff-8dc5-15b41dbaf4ec)

역시나.. 될 리가 없다.. 답을 대놓고 줄 리가 없다. 

이번에는 app.py을 유심히 보았다. 

app.py
```python
from flask import Flask, render_template, request
import subprocess
import re
import time

app = Flask(__name__)
blacklist = set('flag/')
command_executed = False
last_execution_time = 0

def is_valid_command(command):
    if any(char in blacklist for char in command):
        return False
    return True 

def execute_command(command):
    try:
        result = subprocess.run(command, shell=True, capture_output=True, text=True)
        output = result.stdout.strip()
        error = result.stderr.strip()
        if output:
            return output
        if error:
            return error
    except Exception as e:
        return str(e)

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/execute_command', methods=['POST'])
def execute_command_route():
    global command_executed, last_execution_time
    current_time = time.time()
    if command_executed and (current_time - last_execution_time) < 30:
        time_left = 30 - (current_time - last_execution_time)
        return f"You've already executed a command! Please wait {int(time_left)} seconds before trying again."
    command = request.form['command']
    if not is_valid_command(command):
        return "try harder!"
    result = execute_command(command)
    command_executed = True
    last_execution_time = current_time
    return result

if __name__ == '__main__':
    app.run(debug=True, port=5678)
```
확장자가 py이니 파이썬 코드인 것은 잘 알겠다. 여기서 알 수 있는 것을 알아보려 했다. 
어느정도 읽어보니 app.py는 index.html, 즉 web shell 사이트에 관한 코드인 것 같다는 생각이 들었다. 
특히 
'You've already executed a command! Please wait {int(time_left)} seconds before trying again.'
부분에서 그렇다는 생각이 들었다. shell command에 정말 여러가지 시도를 해 보았는데 이런 문구를 정말 많이 보았다. 
읽어 보니, 한번 command shell에 입력을 해보고 그 다음에 입력할때 30초가 지나지 않으면 이 문구가 뜨는 것 같다. 
게다가 'try harder' 라는 문구도 워낙에 많이 봐서 더 그렇다는 확신이 들었다. 

또,
```python
blacklist = set('flag/')
```
을 보니 'flag/'는 입력하면 안되는 것 같다. 

그리고 app.py 뿐만 아니라 dockerfile에서도 flask라는 말이 많이 등장하길래 꽤 중요한 것으로 보였다. 


dockerfile
```python
FROM python:3.8

WORKDIR /app
COPY . /app

RUN apt-get update
RUN pip3 install --upgrade pip
RUN pip3 install flask
EXPOSE 5050
apt
ENV FLASK_APP app/app.py

CMD ["flask", "run", "--host", "0.0.0.0", "--port", "5678"]
```

검색을 해보니 flask는 파이썬으로 작성된 마이크로 웹 프레임워크라고 한다. 사용하려면 설치를 해야한다고 한다. 
flask를 어떻게 쓸지는 모르겠지만 설치를 해 보았다. 
![스크린샷 2024-04-28 142950](https://github.com/hyemsnail/Space_WAR/assets/163375128/f545670f-b358-49fa-9d3b-9730e8fb6fff)

그러다 dockerfile에 flask를 설치하는 것 같은 코드가 보여서 다시 한번 해 보았다. 
![스크린샷 2024-04-28 143502](https://github.com/hyemsnail/Space_WAR/assets/163375128/8da5b66d-16a7-483f-a243-8d2c99e540b0)

에러가 뜨고 거기서 시키는 대로 다시 한번 해 보았다. 
![스크린샷 2024-04-28 143509](https://github.com/hyemsnail/Space_WAR/assets/163375128/8d433d35-7a15-4e23-9199-cd1fc7c4939f)
![스크린샷 2024-04-28 143517](https://github.com/hyemsnail/Space_WAR/assets/163375128/a2544cfe-236b-4769-86fd-0e86fbd77bef)

already satisfied라고 뜨는 것을 보니 아까 dockerfile에 나와있는대로 하기 전 설치했던 것이 제대로 설치가 되긴 된 모양이다. 

docker-compose.yml파일은 
```python
version: '3'

services:
  web:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "5678:5678"
    volumes:
      - ../for_organizer:/app
    environment:
      - FLASK_APP=app/app.py
      - FLASK_ENV=development
```
이것인데 이것은 어떤 내용을 어떻게 파악해야하는지 아예 감도 오지 않는다. 
내가 이번 CTF에서 해본 것은 여기까지 이다. 이번에는 app.py의 내용을 어느정도 해석한 것 처럼 저번 보다는 내용을 아주아주 조금은 더 이해를 한 상태인 것 같다. 나머지 모르는 부분은 다른 분께서 올리시는 write up을 참고해야겠다. 





