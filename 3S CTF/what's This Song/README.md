what's This Song
=================
파일들 중 output.txt를 열면 암호화된 문자들이 쭉 나온다.<br/>
아마도 이것이 랜섬웨어에 의해 암호화된 것 같다. <br/>
hint.txt 파일을 보니 '빈도 분석' 이라는 것을 이용하는 것 같다. <br/>
빈도 분석은 평문과 암호문에 사용되는 문자 또는 문자열의 출현 빈도를 단서로 이용하는 암호해독법이라고 한다. <br/>
그러면 일단 output.txt에 사용된 각 문자들의 빈도수를 알아내야 할 것 같다. <br/>
![스크린샷 2024-08-18 061444](https://github.com/user-attachments/assets/a454ca4b-a79e-47d2-b36c-87f683a74a94) <br/>
자료 조사 후에 나온 빈도수 분석 사이트에 암호문을 넣어보았다. d가 제일 많다고 한다. <br/>
그런데 여기는 숫자도 많은데 알파벳만 분석이 된 것 같다. 그래서 숫자까지도 분석을 할 수 있는 분석기를 알아보았는데 없다...<br/>
애초에 빈도수 분석법은 통계학상으로 알파벳들이 쓰이는 회수가 똑같지 않다는 사실에서 착안한 방법이라고 한다. 그래서 숫자가 없는 것 아닌 가 싶다. <br/>
숫자를 어떻게 처리를 해야 하는지 모르겠다...<br/>
힌트에 아스키 코드도 있었는데 마냥 그걸로 바꾸기 어려운게 숫자들도 연속으로 여러개가 이어져 있어서 어느정도에서 끊어 바꿔야 할지 잘 모르겠다...<br/><br/>
malware.py 파일을 확인해 보았다. <br/>
이 프로그램은 input.txt에서 입력된 텍스트를 암호화하고 output.txt 파일에 저장하는 것 같다. <br/>
암호화 과정을 보니 랜덤하게 바꾸는 것 같다. 랜덤하게 바꿀 경우는 어떻게 해야 할지 좀 막막하다...


