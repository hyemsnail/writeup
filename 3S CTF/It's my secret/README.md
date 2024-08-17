It's my secret
==============
nox를 사용하라고 해서 다운받은 apk-debug 파일을 nox에 설치하고 열어보았다.<br/>
nox에 설치하면 앱 이름이 SecurityFactorial(추정) 이 있다. <br/>
![스크린샷 2024-08-18 051926](https://github.com/user-attachments/assets/751f06c8-62d7-4f2b-952f-f65bf81283c2) <br/>

![스크린샷 2024-08-18 051101](https://github.com/user-attachments/assets/4cad14b2-c919-4efe-ae07-f89d6a6ebe88) <br/>
밑에 버튼을 누르면 한 문장씩 아래에 나온다. 처음 인사를 하고 안드로이드가 처음이냐 물어보고 쉽다고 한다. <br/><br/>
이 다음부터는 어떻게 하는지 전혀 몰라서 자료 조사를 한 후 https://sseddi.tistory.com/183 블로그를 참고하기로 했다. <br/>
이 분처럼 나도 Jadx 디컴파일러를 설치하고 거기서 apk 파일을 열어보았다. <br/>
많은 파일들이 있다. 여기서 어떤 것을 봐야 할지 선택을 해야 할 것 같은데 example.securityfactorial 파일에 secretActivity 파일이 있다. 비밀이라고 하니 제일 수상해 보였다. <br/>
그 파일을 열어보니 아래 사진처럼 플래그 처럼 보이는 것이 나왔다. <br/>
![스크린샷 2024-08-18 051519](https://github.com/user-attachments/assets/92a104d3-1fae-4cb6-b635-e49221d479c1) <br/>
플래그는 ```SF{It's_your_first_step_toward_Android_hacking}```이다. 

