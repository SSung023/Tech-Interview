## 개발상식, 기타

<details>
  <summary><h3>1. 가상화가 무엇이고, 이것이 가상머신과 어떠한 차이가 있는지 설명해 주세요.</h3></summary>
<details>
<summary>자세히</summary>
가상화란, 물리적인 컴퓨터 자원을 소프트웨어적으로 추상화하여, 여러 가상 자원을 생성하는 기술입니다. 이를 통해 여러 개의 운영체제나 어플리케이션을 동시에 실행할 수 있습니다. <br>
가상 머신은 "가상화 기술을 이용"해 하드웨어를 소프트웨어적으로 표현한 환경입니다. 각 가상 머신은 독립된 운영체제와 어플리케이션을 실행할 수 있으며, 서로 격리되어 있습니다. <br>
가상화는 자원을 나누는 방법을 이야기하는 것이고, 가상머신은 가상화 기술을 이용하여 만든 독립적인 가상 컴퓨터라고 볼 수 있습니다.
</details>

<ul>
<li> 그렇다면 Docker는 둘 중 어디에 속하나요? 왜 사람들이 Docker를 많이 채택할까요?</li>
<details>
<summary>자세히</summary>
Docker는 가상화 기술의 한 형태로, 컨테이너 기반의 가상화를 제공합니다. Docker는 어플리케이션과 실행에 필요한 요소들을 패키징하여 다른 환경에서도 일관된 실행을 보장합니다. <br>
Docker는 실행에 필요한 요소들만 포함하기 때문에, OS를 포함하는 가상 머신보다 더 가볍습니다. <br>
또한 Docker는 CI/CD 환경에서 매우 유용하며, 배포에 활용할 수 있어 많은 사람들이 Docker를 사용합니다.
</details>

<li> 하나의 Host OS에서 돌아간다면 충분히 한 컨테이너가 다른 컨테이너에 간섭할 수 있는 위험이 있지 않을까요? 이를 어떻게 방어할 수 있을까요?</li>
<details>
<summary>자세히</summary>
하나의 Host OS를 공유한다면, 한 컨테이너가 다른 컨테이너를 간섭할 수 있는 위험이 존재합니다. <br>
이를 방지하기 위해 리눅스의 네임스페이스를 사용하거나, 각 컨테이너 간에 별도의 네트워크 인터페이스를 연결하는 등 네트워크 설정을 통해 방어할 수 있다고 알고 있습니다.
</details>

<li> Docker 위에 Docker를 올릴 순 없을까요?</li>
<details>
<summary>자세히</summary>
직접 사용해본적은 없지만, Docker in Docker를 통해 Docker 위에 Docker를 올릴 수 있는 것으로 알고 있습니다.
</details>

</ul>
</details>

<details>
  <summary><h3>2. CI/CD 를 사용해 본 경험이 있나요? 있다면 간단하게 설명해 주세요.</h3></summary>
<ul>
</ul>
</details>

<details>
  <summary><h3>3. static 키워드는 어떤 의미를 갖나요? (본인이 사용하는 언어에서 없다면 패스...)</h3></summary>
<ul>
<li> 컴파일 할 때, static 키워드가 붙은 변수, 함수는 어떻게 처리되나요?</li>
<li> Java에서 static과 static final은 어떤 차이를 갖나요? final과 static final은요? </li>
</ul>
</details>

<details>
  <summary><h3>4. 객체지향 프로그래밍이 무엇인가요?</h3></summary>
<ul>
<li> SOLID 원칙에 대해 설명해 주세요.</li>
<li> 다형성이 무엇인지 설명하고, 동적 다형성과 정적 다형성이 무엇인지 설명해 주세요.</li>
<li> 오버로딩과 오버라이딩의 차이에 대해 설명해 주세요.</li>
<li> 클래스가 있는 언어는 반드시 객체지향 언어라고 할 수 있을까요? 그 반대는 성립하나요?</li>
</ul>
</details>

<details>
  <summary><h3>5. 프레임워크와 라이브러리의 차이에 대해 설명해 주세요.</h3></summary>
<ul>
</ul>
</details>

<details>
  <summary><h3>6. Call By Value와 Call By Reference의 차이를 본인의 언어를 기반으로 설명해 주세요.</h3></summary>
<ul>
<li> 사실 이 질문에는 약간의 낚시가 있습니다. 과연 모든 언어에 저 개념이 존재할까요?</li>
</ul>
</details>

<details>
  <summary><h3>7. 순수함수가 무엇인지를 함수형 프로그래밍 매커니즘과 연관지어 설명해 주세요.</h3></summary>
<ul>
<li> Side Effect가 무엇인가요? 이를 모두 없애는 프로그래밍이 이상적이라고 할 수 있을까요?</li>
<li> 왜 함수형 프로그래밍 매커니즘을 사용한다고 생각하시나요?</li>
<li> 순수함수는 Thread Safe 한가요? 왜 그럴까요?</li>
<li> 고차함수에 대해 설명해 주세요.</li>
</ul>
</details>

<details>
  <summary><h3>8. MVC 패턴이 무엇인가요?</h3></summary>
<ul>
<li> 다른 아키텍쳐 패턴은 없나요? MVC랑 비교해서 어떤 차이가 있나요?</li>
</ul>
</details>

<details>
  <summary><h3>9. 디자인 패턴이 무엇인지 설명해주고, 대표적인 디자인 패턴에 대해 설명해 주세요.</h3></summary>
<ul>
<li> Singleton의 장단점에 대해 설명해 주세요.</li>
<li> Singleton이 하나의 객체를 생성한다는 것을 어떻게 보장할 수 있을까요?</li>
</ul>
</details>

<details>
  <summary><h3>10. GC에 대해 설명해 주세요.</h3></summary>
<ul>
<li> 본인이 사용하는 언어에서는 GC를 어떻게 구현했나요?</li>
<li> GC의 장단점에 대해 설명해 주세요.</li>
<li> GC는 어떤 영역에 있는 데이터를 관리하나요?</li>
<li> Reference Counting 방식에 대해 설명하고, 이 알고리즘에서 발생할 수 있는 순환 참조 및 Retain Cycle에 대해 설명해 주세요.</li>
</ul>
</details>

<details>
  <summary><h3>11. 32비트와 64비트의 차이는 무엇인가요?</h3></summary>
<ul>
<li> 32비트에서 가용한 메모리의 크기는 최대 4GB라고 하는데, 왜 그런걸까요?</li>
</ul>
</details>

<details>
  <summary><h3>12. 인증과 인가의 차이에 대해 설명해 주세요.</h3></summary>
<ul>
<li> OAuth가 무엇인지 설명하고, 이것은 인증인지 인가인지에 대해 설명해 주세요.</li>
</ul>
</details>

<details>
  <summary><h3>13. JWT 인증 방식이 무엇인가요?</h3></summary>
<ul>
<li> Signature는 어떻게 만들어지나요?</li>
<li> 만약 Access Token이 탈취되면, 어떻게 대응할 수 있을까요?</li>
<li> 반대로 Refresh Token이 탈취되면, 어떻게 대응해야 할까요?</li>
</ul>
</details>

<details>
  <summary><h3>14. 암호화 알고리즘에 대해 설명해 주세요.</h3></summary>
<ul>
</details>

<details>
  <summary><h3>15. 문자열 인코딩에 대해 설명해 주세요.</h3></summary>
<ul>
<li> Base64 인코딩은 일반적인 문자열 인코딩과는 달리, 사용자가 읽기 어려운 알파벳과 숫자 조합으로 변경합니다. 이를 사용하는 이유는 무엇일까요?</li>
</details>

<details>
  <summary><h3>16. Git에 대해 설명해 주세요.</h3></summary>
<ul>
<li> 여러 브랜치를 합쳐야 할 때, 어떤 방법을 사용할 수 있는지 "모두" 설명해 주세요.</li>
<li> 여러 브랜치를 합쳐야 할 때, 어떤 방법을 사용할 수 있는지 "모두" 설명해 주세요.</li>
</details>