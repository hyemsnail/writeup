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
이 문제는 수학 문제를 푼 다음 RSA 암호를 해독하는 문제이니 아마도 key값이 23일 것 같다. <br/>




