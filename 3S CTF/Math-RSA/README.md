Math-RSA
========
수학 문제를 풀어서 RSA 암호를 해독하는 문제이다.<br/>
hint 파일을 읽어보니 조건에 일치하는 숫자는 ```23```이다. 물론 가장 작은 경우가 23이고 더 큰 경우도 있다. 그런데 답이 하나라면 높은 확률로 23일거라 생각한다. <br/><br/>
rsa.txt 파일을 열어보니 이것이 rsa로 암호화된 것 같다. <br/>
파일 내용을 그대로 복사해서 RSA Online 해독 사이트에 넣어보았다. <br/>
![스크린샷 2024-08-16 104613](https://github.com/user-attachments/assets/23828c5a-eee8-4824-bbaa-df5067268faa) <br/>
중간에 Enter Public/Private key가 있는데 무엇을 입력해야 하는지 딱히 모르겠어서 처음에 풀었던 수학 문제의 답 23을 넣어보았다. <br/>
결과가 나온 것을 보니 정상적인 결과는 아닌 것 같다. <br/><br/>
![스크린샷 2024-08-16 104653](https://github.com/user-attachments/assets/553157a2-5335-447b-9aca-eb6d83f1bcf7) <br/>
public key로 바꾸면 혹시 될까 해보았지만 같은 결과가 나왔다. 중간에 Decryption Algorithm도 다른 걸로 다 바꾸어 보았는데 딱히 변화는 없었다. <br/>
다른 해독 사이트도 확인을 해보니 RSA 해독을 할 때 public key 또는 private key가 반드시 필요한 것 같다.<br/>
이 문제는 수학 문제를 푼 다음 RSA 암호를 해독하는 문제이니 아마도 key값이 23일 것 같다. <br/><br/>
어떻게 해야 하는지 찾아보다 https://hackingstudypad.tistory.com/315 를 보게 되었다. 유용할 것 같아서 이 블로그를 시도해 보았다. <br/>
우선 RSA는 엄청나게 큰 숫자일수록 소인수분해가 어렵다는 점에서 착안해 만들어진 것이라고 한다. <br/>
RSA에는 두 소수 p, q가 필요하다. 그리고 그 두 소수에서 1씩 뺀 값과 서로소인 정수 e가 필요하다. 그리고 개인키 d가 필요하다. n=pq를 계산한 n도 필요하다. <br/>
하지만 rsa.txt 파일을 보면 보통은 n이나 e 등의 문자가 들어갈 자리에 text1_1 ~ text3_2 가 있다. 어떤 것이 어떤 문자인지 모르겠다. <br/>
그리고 그냥 번호가 연속적으로 이어지는 것이 아니라 1_1, 1_2, 2_1, 2_2, 3_1, 3_2 이런 식으로 이어져 있어 어떠한 규칙으로 나누었을 것 같긴 하다. <br/>
그리고 소수인 p와 q 값이 rsa.txt에 있을 줄 알았는데 숫자들을 각각 소수 검사기에 돌려보니 소수는 하나도 없었다. <br/>
![스크린샷 2024-08-16 113952](https://github.com/user-attachments/assets/f67769e3-d861-464c-bfef-e7ffdd697260) <br/>
참고 자료에 나온대로 RsaCtfTool을 사용해보려고 했다. 설치를 하면 RsaCtfTool.py 파일이 보이게 된다.<br/><br/>
![스크린샷 2024-08-16 115426](https://github.com/user-attachments/assets/510be1c5-8017-44ad-ab7d-323f7dc0bf65) <br/>
나온대로 옵션을 이용해서 해보려고 했는데 무엇이 n값이고 e값이고 c값인지 몰라 결과가 이상하게 나온다. <br/><br/>
![스크린샷 2024-08-16 121616](https://github.com/user-attachments/assets/38f72887-c8b4-41ab-8c06-8fb609d2e0a4) <br/>
(원래 의도한 것, 이건 내가 한게 아님) <br/>

여기까지가 내가 시도한 부분이다. rsa.txt를 해독하면 된다는 것은 알겠지만 어떻게 해야 하는지는 잘 모르겠다...






