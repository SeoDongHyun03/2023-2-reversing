# basic 1번 #
01.exe를 실행하면 다음과 같은 창들이 나온다.   
<img src="./basic 01/1-1.jpg"> <img src="./basic 01/1-2.jpg">   
그리고 디버깅을 하면 다음과 같은 코드가 나온다.   
<img src="./basic 01/1-3.jpg">   
여기서 **call <JMP&GetDriveTypeA>**을 실행한 return 값(EAX)가 3이다.   
<img src="./basic 01/1-4.jpg">   
**0040101D ~ 00401023**을 보면 **EAX -= 2, ESI += 3**이 되는걸 알 수 있다.   
그리고 **cmp eax, esi**와 **je** 명령어를 통해 **EAX, ESI가 같아야** 원하는 정답을 얻을 수 있다는 것을 알 수 있다.   
따라서 나 같은 경우에는 **EAX를 00401005**로 바꾸었다.   
<img src="./basic 01/1-5.jpg">   
EAX를 바꾸고 **0040101D ~ 00401026**의 명령어들을 실행하면, 다음과 같은 정답임을 알려주는 창이 뜬다.   
<img src="./basic 01/1-6.jpg">   

# basic 2번 #

# basic 3번 #

# basic 4번 #

# basic 5번 #
