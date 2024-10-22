## 운영체제

<details>
  <summary><h3>1. 시스템 콜이 무엇인지 설명해 주세요.</h3></summary>
<details>
<summary>답안</summary>
시스템 콜이란 -> 운영체제(OS)와 사용자 프로그램 간에 `interface` 역할을 하는 함수  <br>
사용자 프로그램이 파일 읽기/쓰기, 프로세스 생성과 같이 kernel의 기능을 사용하고자 할 때 system call을 호출
</details>
<ul>
<li> 우리가 사용하는 시스템 콜의 예시를 들어주세요.</li>
<details>
<summary>자세히</summary>
파일 열기, 읽기, 쓰기와 같은 open(), read(), write() <br>
프로세스를 생성하거나, 새로운 프로그램을 실행할 때에도 system call을 호출합니다.
</details>

<li> 시스템 콜이, 운영체제에서 어떤 과정으로 실행되는지 설명해 주세요.</li>
<details>
<summary>자세히</summary>
1. user mode에서 실행되고 있는 사용자 프로세스에서 필요에 의해 system call을 호출 <br>
2. kernel에세 system call의 정보를 전달. <br>
3. 이 때, 각 system call 별로 식별할 수 있는 고유번호가 있기 때문에, kernel은 고유 번호를 통해 알맞는 서비스 루틴 실행 가능.<br>
kernel은 전달받은 system call에 알맞는 **서비스 루틴** 실행 <br>
4. kernel이 서비스 루틴을 모두 실행한 후, user mode로 다시 반환
</details>

<li> 시스템 콜의 유형에 대해 설명해 주세요.</li>
<details>
<summary>자세히</summary>

</details>

<li> 운영체제의 Dual Mode 에 대해 설명해 주세요.</li>
<details>
<summary>자세히</summary>
운영체제는 kernel mode와 User mode 두 개의 mode로 나누어져 있으며, 이를 Dual mode라고 한다. <br>
kernel mode에서는 시스템에 영향을 줄 수 있는 명령(파일 관리, 프로세스 생성 등) privileged instruction(특권 명령)을 실행할 수 있으며, <br>
user mode는 일반적인 사용자 프로그램 실행 시 사용되며, 시스템에 영향을 줄 수 있는 privileged instruction을 실행하지 못합니다.

</details>

<li> 왜 유저모드와 커널모드를 구분해야 하나요? </li>
<details>
<summary>자세히</summary>
privileged instruction(특권 명령)을 무분별하게 호출하면 시스템에 영향을 줄 수 있기 때문에, <br>
일반적으로 사용자 프로그램은 User mode에서 실행되며, 파일 조작, 프로세스 생성과 같이 시스템에 영향을 줄 수 있는 명령은 kernel mode로 변경해 실행할 수 있도록 합니다.<br>

</details>


<li> 서로 다른 시스템 콜을 어떻게 구분할 수 있을까요?</li>
<details>
<summary>자세히</summary>
kernel 내부에 system call을 구분할 수 있는 고유 번호와 제어 루틴을 정의하여, system call이 호출되었을 때 해당 고유 번호에 해당하는 제어루틴을 실행합니다.
</details>



</ul>
</details>

<details>
  <summary><h3>2. 인터럽트가 무엇인지 설명해 주세요.</h3></summary>
<details>
<summary>자세히</summary>
프로그램을 실행하던 중, 입출력 장치 등에 예외 사항이 발생하여 처리가 필요한 경우에 CPU에게 알려 처리할 수 있도록 하는 것을 이야기합니다. <br>
하드웨어 인터럽트와 소프트웨어 인터럽트로 나뉘며, <br>
하드웨어 인터럽트의 경우 마우스 클릭, 키보드 입력과 같은 하드웨어 장치가 요청을 처리하기 위해 CPU의 작업을 중단하고, 인터럽트 처리 루틴을 통해 입력 데이터를 처리합니다. <br>
소프트웨어 인터럽트는 CPU(프로세서)의 처리가 필요함을 알리는 방법으로, 프로그램에서 예외가 발생하거나, system call을 호출하기 위해 사용됩니다.<br>
</details>

<br>

<details>
<summary>trap과 interrupt</summary>
소프트웨어 인터럽트(내부 인터럽트)는 trap과 svc interrupt로 나뉠 수 있습니다. <br>
먼저 trap은 주로 예외(exception)이나 오류(error)가 발생했을 때 CPU가 자동으로 발생시키는 소프트웨어 인터럽트이다. <br>
프로그램의 실행이 중단되고, CPU는 OS에게 제어권을 넘겨 이 문제를 해결한다. 0으로 나누기, 잘못된 메모리 접근과 같은 예외 생 시 trap이 발생한다. <br>
SVC interrupt는 SuperVisor interrupt의 약자로서, 응용 프로그램이 파일 관리, 메모리 조작과 같이 system call이 필요한 경우 발생된다.
</details>

<ul>
<li> 인터럽트는 어떻게 처리하나요?</li>
<details>
<summary>자세히</summary>
1. 인터럽트 발생 <br>
2. 실행 중이던 명령어 수행 후, 실행 중단<br>
3. 인터럽트 처리 이후 현재 프로그램에 복귀하기 위해, PC(Program Counter)의 값을 PCB에 저장<br>
4. 인터럽트 벡터에서 인터럽트 번호를 통해 인터럽트 처리 루틴(ISR)을 찾은 후 실행<br>
5. PCB의 PC(Program Counter)를 통해 프로세스가 이전으로 실행했던 위치로 복원<br>
6. 이전에 실행했던 프로세스의 실행 재개
</details>

<li> Polling 방식에 대해 설명해 주세요.</li>
<details>
<summary>자세히</summary>
CPU가 주기적으로 장치 / 자원의 상태를 확인하여 어떤 작업이 필요한지 검사하고 실행하는 방식입니다. <br>
장치가 직접 신호를 보내는 것이 아닌, CPU가 스스로 확인하는 방법입니다. <br>
구현이 단순하다는 장점이 있지만, 계속해서 상태를 확인하기 때문에 자원을 불필요하게 소모하는 오버헤드가 발생하는 단점이 있습니다.
</details>

<li> HW / SW 인터럽트에 대해 설명해 주세요.</li>
<details>
<summary>자세히</summary>
위에 적어놨음
</details>

<li> 동시에 두 개 이상의 인터럽트가 발생하면, 어떻게 처리해야 하나요? </li>
<details>
<summary>자세히</summary>
동시에 여러 개의 인터럽트가 발생했을 때 처리하는 방법을 크게 두 가지로 나눠보면 우선순위를 통해 판별하는 방법과, 인터럽트를 중첩하는 방법이 있습니다. <br>
각각의 인터럽트에는 우선순위가 있는데, 여러 개의 인터럽트가 동시에 발생했을 때 우선순위가 높은 인터럽트를 먼저 처리하며, 우선순위가 낮은 인터럽트는 앞의 인터럽트들이 처리 될 때까지 대기하는 방법입니다. <br>
인터럽트 중첩은 인터럽트 처리 도중에...
</details>

</ul>
</details>

<details>
  <summary><h3>3. 프로세스가 무엇인가요?</h3></summary>
<ul>
<li> 프로그램과 프로세스, 스레드의 차이에 대해 설명해 주세요.</li>
<li> PCB가 무엇인가요?</li>
<li> 그렇다면, 스레드는 PCB를 갖고 있을까요?</li>
<li> 리눅스에서, 프로세스와 스레드는 각각 어떻게 생성될까요?</li>
<li> 자식 프로세스가 상태를 알리지 않고 죽거나, 부모 프로세스가 먼저 죽게 되면 어떻게 처리하나요?</li>
<li> 리눅스에서, 데몬프로세스에 대해 설명해 주세요.</li>
<li> 리눅스는 프로세스가 일종의 트리를 형성하고 있습니다. 이 트리의 루트 노드에 위치하는 프로세스에 대해 설명해 주세요.</li>
</ul>
</details>

<details>
  <summary><h3>4. 프로세스 주소공간에 대해 설명해 주세요.</h3></summary>
<ul>
<li> 초기화 하지 않은 변수들은 어디에 저장될까요?</li>
<li> 일반적인 주소공간 그림처럼, Stack과 Heap의 크기는 매우 크다고 할 수 있을까요? 그렇지 않다면, 그 크기는 언제 결정될까요?</li>
<li> Stack과 Heap 공간에 대해, 접근 속도가 더 빠른 공간은 어디일까요?</li>
<li> 다음과 같이 공간을 분할하는 이유가 있을까요?</li>
<li> 스레드의 주소공간은 어떻게 구성되어 있을까요?</li>
<li> "스택"영역과 "힙"영역은 정말 자료구조의 스택/힙과 연관이 있는 걸까요? 만약 그렇다면, 각 주소공간의 동작과정과 연계해서 설명해 주세요.</li>
<li> IPC의 Shared Memory 기법은 프로세스 주소공간의 어디에 들어가나요? 그런 이유가 있을까요? </li>
<li> 스택과 힙영역의 크기는 언제 결정되나요? 프로그램 개발자가 아닌, 사용자가 이 공간의 크기를 수정할 수 있나요? </li>
</ul>
</details>

<details>
  <summary><h3>5. 단기, 중기, 장기 스케쥴러에 대해 설명해 주세요.</h3></summary>
<ul>
<li> 현대 OS에는 단기, 중기, 장기 스케쥴러를 모두 사용하고 있나요?</li>
<li> 프로세스의 스케쥴링 상태에 대해 설명해 주세요.</li>
<li> preemptive/non-preemptive 에서 존재할 수 없는 상태가 있을까요?</li>
<li> Memory가 부족할 경우, Process는 어떠한 상태로 변화할까요?</li>
</ul>
</details>

<details>
  <summary><h3>6. 컨텍스트 스위칭 시에는 어떤 일들이 일어나나요?</h3></summary>
<ul>
<li> 프로세스와 스레드는 컨텍스트 스위칭이 발생했을 때 어떤 차이가 있을까요?</li>
<li> 컨텍스트 스위칭이 발생할 때, 기존의 프로세스 정보는 커널스택에 어떠한 형식으로 저장되나요?</li>
<li> 컨텍스트 스위칭은 언제 일어날까요?</li>
</ul>
</details>

<details>
  <summary><h3>7. 프로세스 스케줄링 알고리즘에는 어떤 것들이 있나요?</h3></summary>
<ul>
<li> RR을 사용할 때, Time Slice에 따른 trade-off를 설명해 주세요.</li>
<li> 싱글 스레드 CPU 에서 상시로 돌아가야 하는 프로세스가 있다면, 어떤 스케쥴링 알고리즘을 사용하는 것이 좋을까요? 또 왜 그럴까요?</li>
<li> 동시성과 병렬성의 차이에 대해 설명해 주세요.</li>
<li> 타 스케쥴러와 비교하여, Multi-level Feedback Queue는 어떤 문제점들을 해결한다고 볼 수 있을까요?</li>
<li> FIFO 스케쥴러는 정말 쓸모가 없는 친구일까요? 어떤 시나리오에 사용하면 좋을까요? </li>
<li> 우리는 스케줄링 알고리즘을 "프로세스" 스케줄링 알고리즘이라고 부릅니다. 스레드는 다른 방식으로 스케줄링을 하나요?</li>
<li> 유저 스레드와 커널 스레드의 스케쥴링 알고리즘은 똑같을까요?</li>
</ul>
</details>

<details>
  <summary><h3>8. 뮤텍스와 세마포어의 차이점은 무엇인가요?</h3></summary>
<ul>
<li> 이진 세마포어와 뮤텍스의 차이에 대해 설명해 주세요.</li>
<li> Lock을 얻기 위해 대기하는 프로세스들은 Spin Lock 기법을 사용할 수 있습니다. 이 방법의 장단점은 무엇인가요? 단점을 해결할 방법은 없을까요?</li> 
<li> 뮤텍스와 세마포어 모두 커널이 관리하기 때문에, Lock을 얻고 방출하는 과정에서 시스템 콜을 호출해야 합니다. 이 방법의 장단점이 있을까요? 단점을 해결할 수 있는 방법은 없을까요?</li>
</ul>
</details>

<details>
  <summary><h3>9. Deadlock 에 대해 설명해 주세요.</h3></summary>
<ul>
<li> Deadlock 이 동작하기 위한 4가지 조건에 대해 설명해 주세요.</li>
<li> 그렇다면 3가지만 충족하면 왜 Deadlock 이 발생하지 않을까요?</li>
<li> 어떤 방식으로 예방할 수 있을까요?</li>
<li> 왜 현대 OS는 Deadlock을 처리하지 않을까요?</li>
<li> Wait Free와 Lock Free를 비교해 주세요.</li>
</ul>
</details>

<details>
  <summary><h3>10. 프로그램이 컴파일 되어, 실행되는 과정을 간략하게 설명해 주세요.</h3></summary>
<ul>
<li> 링커와, 로더의 차이에 대해 설명해 주세요.</li>
<li> 컴파일 언어와 인터프리터 언어의 차이에 대해 설명해 주세요.</li>
<li> JIT에 대해 설명해 주세요.</li>
<li> 본인이 사용하는 언어는, 어떤식으로 컴파일 및 실행되는지 설명해 주세요.</li>
<li> Python 같은 언어는 CPython, Jython, PyPy등의 다양한 구현체가 있습니다. 각각은 어떤 차이가 있을까요? 또한, 실행되는 과정 또한 다를까요?</li>
<li> 우리는 흔히 fork(), exec() 시스템 콜을 사용하여 프로세스를 적재할 수 있다고 배웠습니다. 로더의 역할은 이 시스템 콜과 상관있는 걸까요? 아니면 다른 방식으로 프로세스를 적재할 수 있는 건가요?</li>
</ul>
</details>

<details>
  <summary><h3>11. IPC가 무엇이고, 어떤 종류가 있는지 설명해 주세요.</h3></summary>
<ul>
<li> Shared Memory가 무엇이며, 사용할 때 유의해야 할 점에 대해 설명해 주세요.</li>
<li> 메시지 큐는 단방향이라고 할 수 있나요?</li>
</ul>
</details>

<details>
  <summary><h3>12. Thread Safe 하다는 것은 어떤 의미인가요?</h3></summary>
<ul>
<li> Thread Safe 를 보장하기 위해 어떤 방법을 사용할 수 있나요?</li>
<li> Peterson's Algorithm 이 무엇이며, 한계점에 대해 설명해 주세요.</li>
<li> Race Condition 이 무엇인가요?</li>
<li> Thread Safe를 구현하기 위해 반드시 락을 사용해야 할까요? 그렇지 않다면, 어떤 다른 방법이 있을까요?</li>
</ul>
</details>

<details>
  <summary><h3>13. Thread Pool, Monitor, Fork-Join에 대해 설명해 주세요.</h3></summary>
<ul>
<li> Thread Pool을 사용한다고 가정하면, 어떤 기준으로 스레드의 수를 결정할 것인가요? </li>
<li> 어떤 데이터를 정렬 하려고 합니다. 어떤 방식의 전략을 사용하는 것이 가장 안전하면서도 좋은 성능을 낼 수 있을까요?</li>
</ul>
</details>

<details>
  <summary><h3>14. 캐시 메모리 및 메모리 계층성에 대해 설명해 주세요.</h3></summary>
<ul>
<li> 캐시 메모리는 어디에 위치해 있나요?</li>
<li> L1, L2 캐시에 대해 설명해 주세요.</li>
<li> 캐시에 올라오는 데이터는 어떻게 관리되나요?</li>
<li> 캐시간의 동기화는 어떻게 이루어지나요?</li>
<li> 캐시 메모리의 Mapping 방식에 대해 설명해 주세요.</li>
<li> 캐시의 지역성에 대해 설명해 주세요.</li>
<li> 캐시의 지역성을 기반으로, 이차원 배열을 가로/세로로 탐색했을 때의 성능 차이에 대해 설명해 주세요.</li>
<li> 캐시의 공간 지역성은 어떻게 구현될 수 있을까요? (힌트: 캐시는 어떤 단위로 저장되고 관리될까요?) </li>
</ul>
</details>

<details>
  <summary><h3>15.메모리의 연속할당 방식 세 가지를 설명해주세요. (first-fit, best-fit, worst-fit)</h3></summary>
<ul>
<li> worst-fit 은 언제 사용할 수 있을까요?</li>
<li> 성능이 가장 좋은 알고리즘은 무엇일까요?</li>
</ul>
</details>

<details>
  <summary><h3>16. Thrashing 이란 무엇인가요?</h3></summary>
<ul>
<li> Thrashing 발생 시, 어떻게 완화할 수 있을까요?</li>
</ul>
</details>

<details>
  <summary><h3>17. 가상 메모리란 무엇인가요?</h3></summary>
<ul>
<li> 가상 메모리가 가능한 이유가 무엇일까요?</li>
<li> Page Fault가 발생했을 때, 어떻게 처리하는지 설명해 주세요.</li>
<li> 페이지 크기에 대한 Trade-Off를 설명해 주세요.</li>
<li> 페이지 크기가 커지면, 페이지 폴트가 더 많이 발생한다고 할 수 있나요?</li>
<li> 세그멘테이션 방식을 사용하고 있다면, 가상 메모리를 사용할 수 없을까요?</li>

</ul>
</details>

<details>
  <summary><h3>18. 세그멘테이션과 페이징의 차이점은 무엇인가요?</h3></summary>
<ul>
<li> 페이지와 프레임의 차이에 대해 설명해 주세요.</li>
<li> 내부 단편화와, 외부 단편화에 대해 설명해 주세요.</li>
<li> 페이지에서 실제 주소를 어떻게 가져올 수 있는지 설명해 주세요.</li>
<li> 어떤 주소공간이 있을 때, 이 공간이 수정 가능한지 확인할 수 있는 방법이 있나요?</li>
<li> 32비트에서, 페이지의 크기가 1kb 이라면 페이지 테이블의 최대 크기는 몇 개일까요?</li>
<li> 32비트 운영체제는 램을 최대 4G 까지 사용할 수 있습니다. 이 이유를 페이징과 연관 지어서 설명해 주세요.</li>
<li> C/C++ 개발을 하게 되면 Segmentation Fault 라는 에러를 접할 수 있을텐데, 이 에러는 세그멘테이션/페이징과 어떤 관계가 있을까요? </li> 
</ul>
</details>

<details>
  <summary><h3>19. TLB는 무엇인가요?</h3></summary>
<ul>
<li> TLB를 쓰면 왜 빨라지나요?</li>
<li> MMU가 무엇인가요?</li>
<li> TLB와 MMU는 어디에 위치해 있나요?</li>
<li> 코어가 여러개라면, TLB는 어떻게 동기화 할 수 있을까요? </li>
<li> TLB 관점에서, Context Switching 발생 시 어떤 변화가 발생하는지 설명해 주세요. </li>
</ul>
</details>

<details>
  <summary><h3>20. 동기화를 구현하기 위한 하드웨어적인 해결 방법에 대해 설명해 주세요.</h3></summary>
<ul>
<li> volatile 키워드는 어떤 의미가 있나요?</li>
<li> 싱글코어가 아니라 멀티코어라면, 어떻게 동기화가 이뤄질까요?</li>
<li> 
</ul>
</details>

<details>
  <summary><h3>21. 페이지 교체 알고리즘에 대해 설명해 주세요.</h3></summary>
<ul>
<li> LRU 알고리즘은 어떤 특성을 이용한 알고리즘이라고 할 수 있을까요?</li>
<li> LRU 알고리즘을 구현한다면, 어떻게 구현할 수 있을까요?</li>
<li> LRU 알고리즘의 단점을 설명해 주세요. 이를 해결할 수 있는 대안에 대해서도 설명해 주세요.</li>
</ul>
</details>

<details>
  <summary><h3>22. File Descriptor와, File System에 에 대해 설명해 주세요.</h3></summary>
<ul>
<li> I-Node가 무엇인가요?</li>
<li> 프로그래밍 언어 상에서 제공하는 파일 관련 함수 (Python - open(), Java - BufferedReader/Writer 등)은, 파일을 어떤 방식으로 읽어들이나요?</li>
</ul>
</details>

<details>
  <summary><h3>23. 동기와 비동기, 블로킹과 논블로킹의 차이에 대해 설명해 주세요.</h3></summary>
<ul>
<li> 그렇다면, 동기이면서 논블로킹이고, 비동기이면서 블로킹인 경우는 의미가 있다고 할 수 있나요?</li>
<li> I/O 멀티플렉싱에 대해 설명해 주세요.</li>
<li> 논블로킹 I/O를 수행한다고 하면, 그 결과를 어떻게 수신할 수 있나요? </li>
</ul>
</details>
