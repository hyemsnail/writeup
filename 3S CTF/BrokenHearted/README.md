BrokenHearted
=============
Hint.txt 파일 내용을 보니 '파일 카빙'이라는 것을 해야 하는 것 같다. <br/>
파일 카빙이란 파일 시스템 정보를 사용하지 않고, 파일의 고유 특성만을 이용한 파일 복구 기법을 말한다. 데이터 크기가 존재하지 않는 비할당 영역을 대상으로 수행한다고 한다. <br/>
Hint.txt 파일 말고도 아래 사진과 같은 CTF.jpg 파일 하나가 더 있다. <br/>
![CTF](https://github.com/user-attachments/assets/2d8d247e-58a7-4236-aae1-23df2c56dfcd) <br/><br/>

어떤 것을 이용할까 알아보다가 https://information-security.tistory.com/190 을 참고하여 진행해보기로 했다. <br/>
strings 명령어를 이용해 CTF.jpg 파일의 글자들을 확인해 보았다. <br/>
![스크린샷 2024-08-16 141754](https://github.com/user-attachments/assets/3e241885-aa81-42da-b604-cd5c24267b9b) <br/>
여기서 가장 아래 방향으로 스크롤을 내리면 <br/>
![스크린샷 2024-08-16 141636](https://github.com/user-attachments/assets/8ae87c74-f592-49dd-b912-dc5465079013) <br/>
이런 문구가 나온다. 누구봐도 중요한 힌트이다. LSB 스테가노그래피를 알아보라는 것 같다. <br/>
그리고 Hint2.png 파일과 Hint1.jpg 파일이 있다. 아직은 이름만 보인다. <br/><br/>
binwalk 명령어로 CTF.jpg 파일을 카빙해 보았다. <br/>
![스크린샷 2024-08-16 141826](https://github.com/user-attachments/assets/ec6c9f46-9237-405f-bba8-adce7e1f2185) <br/><br/>
foremost 명령어로 CTF.jpg 파일에 있었던 이미지 파일들을 복구했다. <br/>
![스크린샷 2024-08-16 141835](https://github.com/user-attachments/assets/075aa18c-42c5-42c7-87e0-2cbcad996df7) <br/><br/>
그리고 파일이 있었던 곳에 들어가보니 output이라는 폴더가 새로 생겼다. <br/>
![스크린샷 2024-08-16 142337](https://github.com/user-attachments/assets/d8719ab2-a776-4f13-9e0f-e93da7e8a792) <br/>
output 폴더 안에는 png와 zip파일과 audit.txt 파일이 존재했다. png 파일에는 CTF.jpg 파일과 같은 이미지가 이름만 다르게 존재했고 zip파일에는 <br/>
![스크린샷 2024-08-16 142440](https://github.com/user-attachments/assets/a759a94d-14c4-4aea-83ee-232975c01ccd) <br/>
두가지 파일이 있었다. 한가지 파일에는 flag.bmp 라는 파일이 있었고 아래와 같이 나왔다. <br/>
![스크린샷 2024-08-16 142354](https://github.com/user-attachments/assets/84f7d012-107a-4a1b-8d52-dd4e9a1a8e15) <br/>
또 다른 파일에는 Hint1.jpg 파일과 Hint2.png 파일이 있었다. <br/><br/>
Hint1.jpg 파일<br/>
![스크린샷 2024-08-16 142410](https://github.com/user-attachments/assets/1a765f17-cade-4693-8b7d-2def6d753f29) <br/><br/>
Hint2.png 파일 <br/>
![스크린샷 2024-08-16 142423](https://github.com/user-attachments/assets/b95d1305-bd5a-4849-9ecc-f6a80db7c716) <br/><br/>

flag.bmp 파일과, Hint1.jpg, Hint2.png 파일을 hxd로 열어보았다.<br/>
![스크린샷 2024-08-16 180652](https://github.com/user-attachments/assets/7f271e7d-2905-4892-a88b-7d9a396ac8e0) <br/>
flag.bmp 파일의 가장 아랫부분을 보니 이런 문구가 있었다. 플래그는 FE로 시작하고 00000100 부터 00005000까지를 보면 된다. 216 바이트로 이루어져 있다고 한다.  <br/><br/>
FE로 시작하는 부분을 찾아보았는데 애초에 FE가 있는 부분이 아래 블럭을 친 이 부분 밖에 없다. <br/>
![스크린샷 2024-08-16 182642](https://github.com/user-attachments/assets/1195c245-fb6a-4f62-812f-5a995fcecd07) <br/>
이 부분이 플래그인 것 같다. 근데 이 상태 그대로는 아닐 것 같다. 어떻게든 바꿔야 할 것 같다. 그런데 여기서 어떻게 더 해야하는지 모르겠다... <br/><br/>
원래 여기까지 했다가 다음 날 다른 분의 라이트업을 보았는데 FE와 FF를 치환을 하면 된다는 것을 알게 되었다.<br/>
그 생각을 어떻게 하신 거지...존경스럽다. <br/>
그리고 전체 크기가 216바이트라는 힌트가 있었다. 한줄에 16바이트인데 이것을 둘로 나누어 8바이트씩 27줄을 만들면 되는 것이었다...
그래서 일단 나도 치환을 해 보았다. FE를 0, FF를 1로 치환해 보았다. <br/>
그래서 위에 블럭을 친 부분을 8바이트씩 27줄로 바꿔보았다. <br/>
00110011 <br/>
01010011 <br/>
01111011 <br/>
01100110 <br/>
00110000 <br/>
01100101 <br/>
0110110 <br/>
01110011 <br/>
00110001 <br/>
01100011 <br/>
01110011 <br/>
01011111 <br/>
00110001 <br/>
01110011 <br/>
01011111 <br/>
01010010 <br/>
01100101 <br/>
00110110 <br/>
01101100 <br/>
01101100 <br/>
01111001 <br/>
01011111 <br/>
01000110 <br/>
01010101 <br/>
01101110 <br/>
01111101 <br/><br/>
위의 2진수 숫자들을 각각 아스키 코드로 바꿔주면 <br/>
```3S{f06ens1cs_1s_Re6lly_FUn}```이다. 

















