Wat ch
======
apps.rw 폴더를 통째로 vscode에서 열어보았다. 파일이 정말 많다. <br/><br/>
먼저 여기서 어플리케이션의 개수를 찾아보았다. <br/>
![스크린샷 2024-08-18 064259](https://github.com/user-attachments/assets/73da2776-8140-4830-9020-46e82fa57fdf) <br/>
쭉 내리면서 AppName이 얼마나 나오는지 세어보면 된다. 21개다. <br/>
3번째 리마인더 작성 시간은 reminderConsumerLog에 있었다. 아마도 start를 기준으로 리마인더가 작성되는 듯 하다. <br/>
![스크린샷 2024-08-18 065331](https://github.com/user-attachments/assets/cddb8f66-e096-4d24-8930-ec1ad2df29a7) <br/>
3번재 리마인더 작성 시간은 22:45:48이다. <br/>
음악 파일 명은 MpPlayingList.dat에 있었다. 파일명은 Over the Horizon.mp3이다. <br/>
![스크린샷 2024-08-18 103246](https://github.com/user-attachments/assets/1d8cb415-f216-4ef6-a0e0-6e62e8214b03) <br/>
김소리의 거주지는 날씨가 어느 지역을 기준으로 되어있는지를 확인하면 된다. weather에서 확인할 수 있다. <br/>
그런데 weather에서 그냥 열리는 파일이 없었다. 여기서 시간이 좀 걸렸다. <br/>
vscode가 아닌 다른 툴을 이용해야 할 것 같아 https://yum-history.tistory.com/274 를 참고하여 DB browser for SQLlite를 설치했다. <br/>
여기서 weather db 파일을 열어보았다. <br/>
![스크린샷 2024-08-18 110755](https://github.com/user-attachments/assets/6bb94d8a-0697-4719-91dc-3e141ab18b68) <br/>
대한민국 하남시를 기준으로 되어 있다. 거주지는 대한민국 하남시이다. <br/>
마지막으로 1695650088에 뉴스를 발행한 author를 찾아야한다. <br/>
뉴스 발행이니 magazine 파일의 db를 열어보았다. <br/>
여기서 메뉴가 여러가지 있는데 stories로 하면 번호들이 쭉 나온다. <br/>
![스크린샷 2024-08-18 114539](https://github.com/user-attachments/assets/edfe23b5-145a-4d5a-b9f4-76255d30ae32) <br/>
뉴스를 발행한 곳은 세계일보이다. <br/>
플래그는 ```3S{21_22:45:48_Overthehorizon_대한민국하남시_세계일보}``` 이다. 



