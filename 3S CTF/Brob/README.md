Brob
====
문제 설명으로 bof + probability 라고 나와있었다. <br/>
아마도 bof는 버퍼 오버플로우 일 것 으로 추정이 되고 probability는 말 그대로 확률일 것 같다. 딱히 감이 잡히지는 않는다. <br/><br/>
뭐라도 해보자는 마음으로 brob 파일을 실행시켜 보았다. 아무것도 나오지 않는다.<br/>
![스크린샷 2024-08-17 125125](https://github.com/user-attachments/assets/eedeb5fa-be21-4f9a-aff0-7c6b079f0907) <br/>
커서 자리에 무언가를 입력을 하면 그냥 입력한 것이 한번 더 출력이 되고 밑에 알 수 없는 문자가 나온다. <br/><br/>
버퍼 오버플로우는 분명 중요한 힌트일 것 같아서 자료를 좀 찾아보았고 https://hackingstudypad.tistory.com/105 을 참고해보기로 했다. <br/>
포너블에서 많이 쓰인다는 gdb


