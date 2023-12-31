# 10월 9일 스터디(과제)
## 메모리 구조
![메모리구조](https://www.tcpschool.com/lectures/img_c_memory_structure.png)   
메모리에는 코드, 데이터, 힙, 스택 영역이 있다.   
* 코드 영역 : 컴파일된 바이너리가 실행될 때, 어셈블리어 코드가 코드 영역에 올라간다. -> **실행될 코드가 저장되는 영역**, 텍스트 영역이라고도 부름   
* 데이터 영역 : **전역 변수, static 변수**가 여기에 저장된다. -> c언어에서 static 변수, 상수 배열, 문자열 등이 저장됨   
* 힙 영역 : 동적 할당을 수행할 때, 힙 영역을 사용한다. -> c언어에서 malloc, free를 통해 힙 영역에 **동적 할당하거나 해제**할 수 있다.   
* 스택 영역 : 지역 변수가 존재하는 영역 -> **지역 변수와 매개변수가 저장**되는 영역이다.   

## 레지스터
CPU 내에서 빠르게 데이터를 처리하기 위한 공간   **범용 레지스터, 세그먼트 레지스터, EFLAGS 레지스터** 등이 있다.   (https://vallhalla-edition.tistory.com/24 도 참고했습니다.)

### 범용 레지스터
1. 산술 연산 제지스터
  * eax : **산술연산, 함수 return값**에 사용
  * ebx : **간접 번지 지정, 연산**에 사용
  * ecx : 반복문에서 **Loop Counter**로 사용
  * edx : eax를 보조, **32bit** 시스템에서 **8byte(64bit) 값을 저장**해야할 때 사용(부호 확장)
2. 인덱스 레지스터
  * esi : **데이터 복사, 이동, 출발지 주소를 저장**하는 레지스터
  * edi : **데이터 복사, 이동, 도착지 주소를 저장**하는 레지스터   물론 이 외에도 다른 상황에서도 사용할 수 있다.(임시 저장, 산술 연산 등등)
3. 포인터 레지스터
  * esp : **스택 frame 구성, ebp보다 낮은 주소, 스택이 쌓일 때마다 값이 감소**, 메모리 **스택의 끝 지점 주소** 포인터
  * ebp : **스택 frame 구성, esp보다 높은 주소, 데이터 사용 시 기준이 되는** 레지스터, ebp 주소 밑에 **Return Address 존재**, 메모리 **스택의 첫 시작 주소** 포인터
  * eip : **현재 실행하는 명령어**를 가르키는 레지스터   

범용 레지스터는 상황에 따라 크기가 달라진다.(예 : AX : 16비트, AX = AH:AL(각 8비트씩))


### EFLAGS 레지스터
1. 플래그 레지스터(https://brian3632.tistory.com/entry/%ED%94%8C%EB%9E%98%EA%B7%B8-%EB%A0%88%EC%A7%80%EC%8A%A4%ED%84%B0Flag-Register 참고)
  * CF(Carry Flag) : 최근 연산 결과에서 **받아내림 발생 시 1**로 설정 -> **Unsigned overflow**가 발생할 때 1로 세팅  
  * PF(Parity Flag) : 최근 연산 결과가 **짝수 -> 1, 홀수 -> 0**으로 설정(**1인 비트의 수가 짝수이면 1**이라는 말이 많아서 일단 이렇게 아는 게 좋을 듯)
  * ZF(Zero Flag) : 최근 연산 결과가 **0이면 1**로 설정
  * SF(Sign Flag) : 최근 연산 결과가 **음수 -> 1**로 설정 -> 연산결과의 **MSB(Most Significant Bit)와 같다.**  
  * OF(Overflow Flag) : 최근 연산 결과가 **오버플로우 발생 시 1**로 설정

## 어셈블리어
기계어를 사람이 이해할 수 있도록 1:1 매칭시켜주는 언어
1. 어셈블리어 종류(https://d41jung0d.tistory.com/33 , https://nightohl.tistory.com/entry/imul-assembly 참고)
* PUSH : **esp값 감소, 스택에 데이터 적재**
* POP : **스택 최상단의 데이터를 레지스터에 옮기고 esp 값을 증가**
* MOV : mov a, b -> **b의 '데이터'가 a로 이동**
* LEA : lea a, b -> **b의 '메모리 주소'가 a로 이동**
* ADD : add a, b -> **a = a + b**
* SUB : sub a, b -> **a = a - b**
* IMUL : 부호 있는 곱셈
  * IMUL 목적지(크기에 따라 다름)
    * 목적지가 **byte** : AX = 목적지 * AL
    * 목적지가 **word** : DX:AX = 목적지 * AX
    * 목적지가 **dword** : EDX:EAX = 목적지 * EAX
  * IMUL 목적지, 소스 : **목적지 = 목적지 * 소스**, 마찬가지로 **넘치는 값은 EDX**에 저장
  * IMUL 목적지, 소스, 정수 : **목적지 = 소스 * 정수**, **넘치는 값은 EDX**에 저장
* IDIV : 부호 있는 나눗셈
  * IDIV 소스(8비트 레지스터) : **AX / 소스, AL : 몫, AH : 나머지**
  * IDIV 소스(16비트 레지스터) : **DX:AX / 소스, AX : 몫, DX : 나머지**
  * IDIV 소스(32비트 레지스터) : **EDX:EAX / 소스, EAX : 몫, EDX : 나머지**
* INC : **inc a -> a += 1**
* DEC : **dec a -> a -= 1**
* AND : **and a, b -> a = a & b**
* OR : **or a, b -> a = a | b**
* XOR : **xor a, b -> a = a ^ b**
* JMP : jmp 목적지 -> **목적지로 점프, return address 백업 X**
* JE : je 목적지 -> **ZF = 1이면 목적지로 점프**
* JNE : jne 목적지 -> **ZF = 0이면 목적지로 점프**
* JZ : jz 목적지 -> **ZF = 1 or 연산 결과 = 0이면 jump**
* JNZ : jnz 목적지 -> **ZF = 0 or 연산 결과 != 0이면 jump**
* CMP : cmp a, b -> **a == b이면 CF = 0, ZF = 1로 설정, CF = 0이고 a != b이면, CF = 0**
* JA : cmp a, b -> ja 목적지 -> **a > b이면 목적지로 jump**
* JB : cmp a, b -> jb 목적지 -> **a < b이면 목적지로 jump**
* CALL : call 목적지 -> **return address(eip 값)을 push한 후, 목적지로 이동(함수호출)**
* RET : **함수 종료 후 return address로 돌아감**(나중에 더 자세히 찾아보기) -> 매개변수가 있기도하고 없기도 함

## 디버거 사용법
x64dbg 기준으로 작성함(https://maple19out.tistory.com/6 , https://seoridev.tistory.com/m/3 참고)
1. x64dbg에서 디버깅할 파일을 연다
2. 기능을 이용하여 디버깅을 한다
   * 단축키
     * F2 : **breakpoint(중단점) 생성**
     * F7 : **명령어 한 줄 실행**(함수인 경우, **함수 내부로 들어감**)
     * F8 : **명령어 한 줄 실행**(함수 내부로 **들어가지 않음**)
     * F9 : **프로그램 실행**(**breakpoint 전**까지)
     * Ctrl + g : 사용자가 **입력한 주소로 이동**
     * -, + : 현재 명령어의 **이전/다음 명령어로 이동**(실행/취소 하는거 아님)
     * enter : 분기문에서 **target 주소로 이동**
     * space : **어셈블리어 수정**
     * Ctrl+F2 : 프로그램 **재시작**
     * Alt+F2 : 프로그램 **종료**
 
 
     

