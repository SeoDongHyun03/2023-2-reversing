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
02.exe를 실행하면 다음과 같은 창이 나온다.  
<img src="./basic 02/2-1.jpg">   
문제에 적혀있는 것처럼, 실행파일에 손상이 있다. 즉, 우리가 사용하는 디버거로 문제를 풀 수 없습니다.   
그래서 검색해본 결과 **헥스에디터**라는 프로그램을 사용해야 한다고 해서 설치 후 사용했습니다.(https://m.blog.naver.com/dmsdl814/221951055766 참고했습니다.)  
<img src="./basic 02/2-2.jpg">   
프로그램을 실행해보니, 왼쪽에는 16진수가 나오는 것 같고, 오른쪽에는 decode한 결과를 적은 것 같다.  
<img src="./basic 02/2-3.jpg">  
파일을 분석하던 중, 어셈블리어와 같이 해석된 결과를 볼 수 있었다.  
<img src="./basic 02/2-4.jpg">  
계속 찾던 중, 영어 문장 같은 게 보였다. "Nope, try again!.", "Yeah, you did it!. Crackme #1." 이 보였고, 마지막에 **JK3FJZh**가 있었다.  
뭔가 "Nope, try again!."은 실패했을 때 나올 문구인것 같고, "Yeah, you did it!. Crackme #1."은 성공했을 때 나올 문구처럼 보였다.  
그리고 JK3FJZh는 마지막에 성공한 후, 비밀번호를 주는 것 같았다.  
따라서 **JK3FJZh** 가 우리가 원하는 정답인 비밀번호라고 할 수 있다.  

# basic 3번 #

# basic 4번 #

# basic 5번 #
