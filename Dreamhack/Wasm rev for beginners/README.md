Wasm rev for beginners <br/>
(Dreamhack CTF Season 6 Round #7 (🚩Div1))
=======================
**문제**<br/><br/>
![스크린샷 2024-09-07 225518](https://github.com/user-attachments/assets/abd6d89d-72bb-4e37-93ee-ce9fcd97777d) <br/>

**풀이** <br/>

문제에서 제공된 파일을 압축을 푼 다음 폴더를 열면 ```index.html``` 파일과 ```pkg```라는 폴더가 있다. <br/>
index.html 파일을 열어보면 <br/>
![스크린샷 2024-09-08 215742](https://github.com/user-attachments/assets/2445312d-9d64-4852-99f1-6f087dca5ee9) <br/>
여기다가 알아낸 flag를 입력하는 것 같다. <br/>
이 다음 과정 부터는 정말로 어떻게 하는지 모르겠어서 조사를 해 보았다. <br/>
https://ddddh.tistory.com/136 <br/>
이 글에서는 사실 앞 부분만 그렇구나 하는 마음으로 보고 그 다음 부터는 이해하기 어렵다. 이 자료를 기반으로 추측할 순 있는 것은 index.html 창에 flag 문자열을 입력하고 check 버튼을 누르면 내부적으로 웹어셈블리어 바이너리에서 검증을 할 거라는 것이다. <br/><br/>
pkg 폴더 내부에서 가장 중요해 보이는 파일은 내가 보기에는 .wasm 파일이다. 그래서 wasm이 무엇인지 알아보았다. <br/>
Wasm은 WebAssembly의 줄임말로, 웹 브라우저에서 실행하는 프로그래밍 언어이자 바이트코드이다. C,C++,Rust 시스템 프로그래밍 언어로 작성하고 컴파일한다. JavaScript의 느린 속도를 대체하기 위해 만들어졌고 웹 페이지에서 고성능의 애플리케이션을 사용가능하게 하는 역할이다. <br/><br/>
wasm이 무엇인지 알아낸 다음에도 과정이 막막했다. pkg 폴더에 있는 파일들을 봐선 왠지 JavaScript파일을 다룰 수 있어야 이 문제를 풀 수 있을 것 같기 때문이다. 이 이후에 어떻게 해야 할지 검색을 많이 해 보았는데 그래도 영 감이 안 잡힌다. <br/>
뭐라도 나올까하는 마음으로 hxd에 challenge_bg.wasm을 열어보았다. <br/>
![스크린샷 2024-09-08 222559](https://github.com/user-attachments/assets/575144fe-c540-4ed6-8c8f-4f2e21b7fa58) <br/>
일단 DH...로 시작하는 플래그는 없었고 flag라는 말 자체가 없었다. 그나마 수상해 보이는 부분은 가장 아랫 부분인데 숫자들이 쭉 있고 그 뒤에 language에 대한 말이 있다. 이 wasm파일은 Rust언어로 만들어졌다는 것을 알아냈다. <br/>
이 문제는 어떻게 해결해야하는지 잘 모르겠다. 'beginners'를 위한 문제라고 써 있어 가장 쉬운 문제라고 생각해 이 문제를 시도해 보았지만 어렵게 느껴진다.



