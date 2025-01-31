# CPU의 작동 원리

### 4-1 ALU와 제어장치

###### ALU 결과값

- 레지스터를 통해 피연산자를 받아들이고, 제어장치로부터 수행할 연산을 알려주는 제어 신호를 받아들입니다. 

- 이를 통해 문자, 숫자, 메모리 주소를 결과로 만들어 내며, 결과값은 메모리에 바로 저장되지 않고 레지스터에 일시적으로 저장된다.

- 그 이유는 레지스터 접근 속도보다 메모리 접근 속도가 훨씬 느리기 때문이다. 만약 계속해서 메모리에 접근한다면 실행속도가 매우 느려지게 될 것이다. 그래서 레지스터에 우선 저장된다.

###### ALU 플래그

- 이진수만 봐서는 음수인지 양수인지 판단하기 어렵기 때문에 플래그를 사용한다. 때때로 ALU는 결괏값뿐만 아니라 연산 결과에 대한 추가정보를 내보내야 할 때 플래그 사용

- ex) 부호 플래그, 제로 플래그, 캐리 플래그, 오버플로우 플래그, 인터럽트 플래그, 슈퍼바이저 플래그, 이러한 플래그들은 플래그 레지스터에 저장된다.

###### 제어장치

- 제어 신호를 내보내고, 명령어를 해석하는 부품

###### 제어장치가 받아들이는 정보

1. 제어장치는 클럭 신호를 받아들인다.
   
   클럭신호에 맞추어 제어장치가 작동한다.

2. 제어장치는 해석해야 할 명령어를 받아들인다.
   
   CPU가 해석해야 할 명령어는 명령어 레지스터라는 특별한 레지스터에 저장된다. 제어장치는 이 명령어 레지스터로부터 해석할 명령어를 받아들이고 해석한 뒤, 제어 신호를 발생시켜 부품들의 수행할 내용 알려줌

3. 제어장치는 플래그 레지스터 속 플래그 값을 받아들인다.
   
   플래그 레지스터는 ALU연산의 추가적인 정보여서 이를 해석한 뒤 부품들의 수행할 내용 알려줌

4. 제어장치는 시스템 버스, 그중에서 제어 버스로 전달된 제어 신호를 받아들입니다.
   
   제어 신호는 입출력장치를 비롯한 CPU 외부 장치도 발생시킬 수 있기 때문에 제어장치는 제어 버스를 통해 외부로부터 전달된 제어 신호를 받아들이기도 한다.

###### 제어장치가 내보내는 정보

1. CPU 외부에 전달하는 제어신호
   
   제어 버스로 제어 신호를 내보낸다는 의미와 동일, 이러한 제어 신호에는 메모리에 전달하는 제어 신호와 입출력장치에 전달하는 제어신호가 있다.
   메모리에 값을 R,W하고 싶다면 메모리로, 입출력장치에서 R,W하고 싶다면 입출력장치에 정보 전달

2. CPU 내부에 전달하는 제어 신호

        ALU에 전달하는 제어 신호와 레지스터에 전달하는 제어 신호가 있다.
        ALU에는 수행할 연산을 지시하기 위해, 레지스터에는 레지스터 간에 데이터를 이동시키
        거나 레지스터에 저장된 명령어를 해석하기 위해 제어신호를 내보낸다.





### 4-2 레지스터



###### 프로그램 카운터

- 메모리에서 가져올 명령어의 주소, 즉 메모리에서 읽어 들일 명령어의 주소를 저장한다.



###### 명령어 레지스터

- 해석할 명령어, 즉 방금 메모리에서 읽어 들인 명령어를 저장하는 레지스터이다. 제어장치는 명령어 레지스터 속 명령어를 받아들이고 이를 해석한 뒤 제어 신호를 내보냅니다.



###### 메모리 주소 레지스터

- 메모리의 주소를 저장하는 레지스터이다. CPU가 읽어 들이고자 하는 주소 값을 주소 버스로 보낼 때 메모리 주소 레지스터를 거친다.



###### 메모리 버퍼 레지스터

- 메모리와 주고받을 값을 저장하는 레지스터이다. 즉 메모리에 쓰고 싶은 값이나 메모리로부터 전달받은 값은 메모리 버퍼 레지스터를 거친다. CPU가 주소 버스로 내보낼 값이 메모리 주소 레지스터를 거친다면, 데이터 버스로 주고 받을 값은 메모리 버퍼 레지스터를 거칩니다.



![02장 CPU의 구조와 기능](https://velog.velcdn.com/images/chocaprio/post/988ad875-ece7-4286-8c4c-e4ec98c25ec1/image.png)

대략 실행과정을 그림으로 나타낸 것.





###### 범용 레지스터

- 데이터와 주소를 모두 저장할 수 있는 레지스터, 일반적으로 CPU안에넌 여러 개의 범용 레지스터들이 있고, 현대 대다수 CPU는 모두 범용 레지스터를 가지고 있다.



###### 플래그 레지스터

- 연산 결과 또는 CPU 상태에 대한 부가적인 정보를 저장하는 레지스터이다.



###### 스택 주소 지정 방식

- 스택 방식으로 메모리 저장 공간을 활용한 것

- 메모리 안에 스택처럼 사용할 영역이 정해져 있는데, 이를 **스택영역**이라고 한다.



###### 변위 주소 지정 방식

- 레지스터의 값과 오퍼랜드의 값을 더하여 메모리 주소값을 알아내는 방식

- 그래서 이러한 주소 지정 방식에는 연산코드 + 레지스터 필드+ 오퍼랜드 필드가 존재한다.

- 어떤 레지스터를 더하는지에 따라 상대 주소 지정방식, 베이스 레지스터 주소 지정 방식 등으로 나뉜다.
1. 상대주소 지정방식
   
   - 오퍼랜드와 프로그램 카운터의 값을 더하여 유효 주소를 얻는 방식
   
   - 오퍼랜드가 양수냐 음수냐에 따라 프로그램 카운터가 가리키는 값에서 그값만큼 이동한다.

2. 베이스 레지스터 주소 지정 방식
   
   - 오퍼랜드와 베이스 레지스터의 값을 더하여 유효 주소를 얻는 방식
   
   - 베이스 레지스터가 '기준주소', 오퍼랜드가 '기준 주소로부터 떨어진 거리'이다.







### 4-3 명령어 사이클과 인터럽트

###### 명령어 사이클 : 하나의 명령어를 처리하는 정형화된 흐름

1. 인출 사이클 : 명령어를 메모리에서 CPU로 가져오는 과정

2. 실행 사이클 : 명령어를 CPU에서 실행하는 것 제어장치가 명령어 레지스터에 담긴 값을 해석하고, 제어 신호를 발생시키는 단계가 실행 사이클이다.

3. 간접 사이클 : 명령어를 실행하기 위해 메모리 접근을 한번 더 해야하는 사이클



###### 인터럽트 : 정해진 흐름에 따라 명령어를 처리하지만, 이 흐름이 끊어지는 상황

1. 동기 인터럽트(예외) : CPU에 의해 발생하는 인터럽트, CPU가 실행하는 프로그래밍상의 오류와 같은 예외적인 상황에 마주쳤을 때 발생하는 인터럽트

2. 비동기 인터럽트(하드웨어 인터럽트) : 입출력장치에 의해 발생하는 인터럽트, 입출력장치에서 자신들에게 들어온 정보를 CPU에게 알려 먼저 처리되도록 하는 인터럽트



**하드웨어 인터럽트 처리 순서**

1. 입출력장치는 CPU에 인터럽트 요청 신호를 보냅니다.

2. CPU는 실행 사이클이 끝나고 명령어를 인출하기 전 항상 인터럽트 여부를 확인합니다.

3. CPU는 인터럽트 요청을 확인하고 인터럽트 플래그를 통해 현재 인터럽트를 받아들일 수 있는지 여부를 확인합니다.

4. 인터럽트를 받아들일 수 있다면 CPU는 지금가지의 작업을 백업합니다.

5. CPU는 인터럽트 벡터를 찹조하여 인터럽트 서비스 루틴을 실행합니다.

6. 인터럽트 서비스 루틴 실행이 끝나면 4.에서 백업해 둔 작업을 복구하여 실행을 재개합니다.



인터럽트가 발생할 때 인터럽트 서비스 루틴의 주소를 알아야하는데 이때 이용하는 것이 인터럽트 벡터이다. 인터럽트 벡터는 인터럽트 서비스 루틴의 시작 주소값을 알고 있다. 

추가적으로 인터럽트가 발생하면 그 전에 실행되고 있었던 명령들은 메모리의 스택영역에 저장되어 인터럽트가 종료후 실행된다.




