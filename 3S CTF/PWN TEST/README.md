PWN TEST
========
![스크린샷 2024-08-17 115244](https://github.com/user-attachments/assets/b6861c5e-e8ed-4c6b-8e9b-3c298ae238b1) <br/>
왜인지 모르겠는데 flag가 나와있다...(?) <br/><br/>
칼리 리눅스에서 문제 파일에 있던 prob.py를 실행해보았다. <br/>
![스크린샷 2024-08-17 115613](https://github.com/user-attachments/assets/4af53954-5988-4b8b-910f-559860438222) <br/>
19문제를 통과해야하고 3S를 눌러 시작을 했다. 바로 밑에 암호문 처럼 보이는 것이 길게 나온다. <br/><br/>
![스크린샷 2024-08-17 115650](https://github.com/user-attachments/assets/c537022a-5fe2-425f-bd26-ee5234079d1d) <br/>
10초 정도 지나면 Time out이라는 말이 뜨고 flag를 입력해야 한다. 설명 파일에 나와있던 플래그를 그대로 넣어봤다. 역시 아니었다. <br/><br/>
![스크린샷 2024-08-17 115940](https://github.com/user-attachments/assets/f6081623-99ee-4684-8786-e72613397b36) <br/>
![스크린샷 2024-08-17 115959](https://github.com/user-attachments/assets/43d6ad71-adf9-4f21-b02e-9dce1324cc5c) <br/>
다시 실행을 해보면 통과해야하는 문제 수가 계속 변하는 것을 볼 수 있다. 문제 수는 크게 중요하지 않은 듯 하다. 어느정도 flag를 얻으면 exit하면 될 것 같다. <br/><br/>
![스크린샷 2024-08-17 120721](https://github.com/user-attachments/assets/3197a9fc-28ba-41d0-9de4-3e7be9804d37) <br/>
pwn test 파일을 다시 들어가봤는데 새로운 파일들이 생겼다. c언어 코드 파일과 flag파일이 눈에 띈다. c언어 파일은 열어보니 prob.py 실행 과정에서 입력과 출력을 하고 프로그램 종료까지 하는 것으로 보인다. <br/>
flag파일을 열어보니 flag가 나와있다. 그래서 그대로 복사해서 flag 자리에 넣어보았는데 test1 failed라고만 뜬다. <br/>
애초에 Time out이 오기 전에 무언가를 해야하는 듯 하다. <br/>
실행을 여러번 해봤는데 flag의 값은 항상 달라져있었다. 할 때마다 무작위로 바뀌는 것 같다. <br/><br/>
![스크린샷 2024-08-17 121408](https://github.com/user-attachments/assets/43fdd607-abc7-45cb-b643-be82d0b6a597) <br/>
Time out이 오기전에 exit를 하면 어떻게 될까 궁금하여 시도해보았다. 그냥 똑같이 시간이 흐르고 타임아웃이 된다. <br/><br/>
아무래도 중간에 나오는 저 암호문을 이용하는 것이 맞는 것 같다. prob.py 코드를 보고 힌트를 얻으려고 했다.<br/>
읽어보니 base64로 인코딩 된 바이너리 데이터인 것 같은데...<br/><br/>
base64 디코더에 넣어 보니<br/>
![스크린샷 2024-08-17 120146](https://github.com/user-attachments/assets/60670c0f-09bf-4071-8faa-7df0c41b3c74) <br/>
 영 이상하게 나온다. <br/>
 다른 디코더에도 넣어봤지만 모두 이상하게 나왔다. <br/><br/>
 추정하기로는 10초 안에 저 암호문을 해독해서 Time out이 오기전 빠르게 입력을 하면 그 다음 단계로 넘어가지 않을까 싶다. 여기까지가 내가 시도한 것이다.<br/>
 
















