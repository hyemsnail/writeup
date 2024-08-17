Can solve without thinking
==========================
생각 없이 푸는 문제라고 한다...<br/><br/>
리눅스에서 main 파일을 실행해보았다.<br/>
![스크린샷 2024-08-18 052742](https://github.com/user-attachments/assets/9e41d3bf-d6ca-4ac8-9643-976e947bf162) <br/>
중간에 링크가 하나 나온다. 저기를 들어가보았다. <br/><br/>
![스크린샷 2024-08-18 053121](https://github.com/user-attachments/assets/76c049a1-a75b-4fb3-9d95-2ca72f96cbe4) <br/>
pygame에 관련된 사이트가 하나 뜬다. <br/>
거기서 https://github.com/pygame/pygame?tab=readme-ov-file 로 접근해서 pygame을 설치하고 실행하려 했다. <br/>
설치는 다 된 것 같은데... 마지막 명령인 python3 -m pygame.examples.aliens 를 입력하면 <br/>
![스크린샷 2024-08-18 060216](https://github.com/user-attachments/assets/564ae79f-8c40-4a2b-bf1c-392f1afa648c) <br/>
그냥 나왔던 링크가 또 나온다. 뭔가 이상하다. <br/>
pygame 사이트에서 약간의 튜토리얼을 만들어 놓은 게 있다. <br/>
python 버전을 보니 3 이상이어서 아래와 같은 방식으로 하려고 했다. <br/>
![스크린샷 2024-08-18 055100](https://github.com/user-attachments/assets/67a6275a-d02d-41da-8be8-0635a412c13c) <br/>
위에서부터 차례로 수행했는데 Grab source 부분에서 문제가 생겼다. <br/>
![스크린샷 2024-08-18 055729](https://github.com/user-attachments/assets/08c34814-cc67-4097-9532-d0bfe80900e6) <br/>
권한이 없다고 한다...<br/>
아마 Grab source가 제대로 수행이 되고 난 다음 Run some tests를 수행하여 pygame 문제들을 푸는 것 같다. <br/>
권한 문제가 해결되면 수정해놓겠다...




