# Space WAR #9 Write up

![스크린샷 2024-05-25 185313](https://github.com/hyemsnail/writeup/assets/163375128/423712a8-7974-4151-b384-a9bf3b0e365d)

웹 분야인줄 알았으나 알고보니 포너블이었다... 가장 쉬워 보이는 거 같아서 이 문제를 시도해보았다. 
위의 사진 처럼 파일 두개가 첨부 되어 있다. 첫번재 파일은 flag, dockerfile, prob가 담겨 있고 두 번째 파일은 libc.so.6인데 열어보면 전혀 이게 무슨 말인지 못 알아 듣겠다. 그나마 해석이 조금이라도 가능한건 dockerfile이다. 

```dockerfile
FROM ubuntu:22.04

RUN apt update && apt install socat -y && adduser user --disabled-password

WORKDIR /home/user
EXPOSE 8888

COPY ./flag /home/user/flag
COPY ./prob /home/user/prob

RUN chown -R root:user /home/user && \
    chmod -R 750 /home/user && \
    chmod 744 /home/user/flag

USER user
EXPOSE 8888

ENTRYPOINT ["socat", "TCP-LISTEN:8888,reuseaddr,fork", "EXEC:./prob,pty"]
```


대충 무슨 말인지는 알 것 같은 느낌이다. 순서대로 해보자.

![스크린샷 2024-05-25 190455](https://github.com/hyemsnail/writeup/assets/163375128/184bdc6e-c304-4d32-bcfb-fb28edaf6c40)
![스크린샷 2024-05-25 190522](https://github.com/hyemsnail/writeup/assets/163375128/a0949aa4-e1cb-46e9-b7e0-c75175da4fff)
![스크린샷 2024-05-25 191723](https://github.com/hyemsnail/writeup/assets/163375128/782bcd05-446e-4fda-8bd8-1de2640c9a24)
![스크린샷 2024-05-25 191754](https://github.com/hyemsnail/writeup/assets/163375128/9eb70ac7-5147-47fc-8454-a0210410ec0d)


여기까지는 어찌어찌 된 것 같다. 이 다음부터 어려워졌다. 

---

![스크린샷 2024-05-25 202625](https://github.com/hyemsnail/writeup/assets/163375128/24abb6bd-66b7-449e-9b5d-7d049cd570c0)

사실 정확하게는 잘 모르겠다... 포트 8888번을 열려는 의도를 가지고 한 행동이다. 

- - -
![스크린샷 2024-05-25 203126](https://github.com/hyemsnail/writeup/assets/163375128/af544513-4a85-4194-ae96-91d9f63ff294)

cp를 이용해서 해보려고 했는데 flag 디렉토리가 없다고 해서 하나 만들어봤다. 사실 이걸 내가 직접 만들어야하는지 전혀 확신이 안 든다. 

---
![스크린샷 2024-05-25 205016](https://github.com/hyemsnail/writeup/assets/163375128/2568466b-02b6-4ba9-8634-a358da27aa43)

prob도 한번 만들어 보았다. 

---
![스크린샷 2024-05-25 205544](https://github.com/hyemsnail/writeup/assets/163375128/b2dd2191-f618-4954-aee5-4d1ffe78d05a)

flag디렉토리 안에 파일을 만들어 처음 받은 파일에 flag에 있던 말을 그대로 써봤다.

---

![스크린샷 2024-05-25 205822](https://github.com/hyemsnail/writeup/assets/163375128/870b0772-46f1-4dc6-89ef-97fdf3f3e29a)

그렇게 하고 다시 cp를 시도했지만 안된다...

---

모르겠어서 일단 다음으로 넘어갔다. 

![스크린샷 2024-05-25 210447](https://github.com/hyemsnail/writeup/assets/163375128/d677b7cf-759b-4ef6-a7a6-80b3f56bb15c)
![스크린샷 2024-05-25 210516](https://github.com/hyemsnail/writeup/assets/163375128/5d76b3b0-86bc-4d66-9528-d619d38e9933)

---

![스크린샷 2024-05-25 211239](https://github.com/hyemsnail/writeup/assets/163375128/af462974-ffaf-4f75-b9d2-6aaf5ff5ba31)

socat이 없다고 나와서 설치했다. 

---
![스크린샷 2024-05-25 211738](https://github.com/hyemsnail/writeup/assets/163375128/c62911a8-f81c-40d1-8a9c-d318bf865df2)

그 다음 이렇게 해 봤는데 아무런 반응이 없었다...

flag파일과 libc.so.6파일은 어떻게 사용하는 것일까...
