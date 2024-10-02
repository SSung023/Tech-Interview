### ✅ Compiled 언어란

언어는 `Compiled` 언어와 `Interpreted` 언어로 나뉩니다. 

`Compiled`는 번역으로, `Interpreted`는 통역으로 비유를 해볼 수 있는데요, 

`Compiled` 언어는 개발자가 프로그래밍 언어로 코드를 짜고, 그걸 실행하기 전에 "미리" 컴퓨터가 읽을 수 있는 언어로 번역 작업을 해두는 것을 이야기합니다.

`Interpreted` 언어는 개발자가 작업한 코드를 그대로 컴퓨터에게 건내주면, 통역을 하는 프로그램, 즉 interpreter가 실시간으로 컴퓨터에게 기계어로 통역해서 일을 시키는 것입니다. 실시간 통역과 같은 일을 하는 것이죠.

개발이 더 편하지만, 오류에 취약하고 실행이 더 느리다는 단점이 있습니다.

Java, C, C++, C#과 같은 언어는 Compiled 언어에 속합니다.

그 중 Java는 다른 언어와 달리 JVM이라는 것을 설치해야 하는데요, 이 JVM이 무엇인지 한 번 알아보도록 하겠습니다.

---

### ✅ JVM이란?

#### 🔥 Java compiler

잠깐, 그 전에 Java compiler에 대해 아주 간단하게 알아보고 넘어가겠습니다.

Java compiler는 개발자가 작성한 `고수준의 Java 소스코드`를 JVM(Java Virtual Machine)이 이해할 수 있는 `Java bytecode`로 변환합니다. 

JVM은 이 `Java bytecode`를 OS(운영체제) 플랫폼에 맞는 `기계어(Machine Language)`로 변환하는 작업을 합니다.

#### 🔥 JVM을 왜 써야해?

컴퓨터도 운영체제의 종류에 따라 사용하는 `기계어(Machine Language)`가 다릅니다.

쉽게 이야기해서 윈도우, 맥, 리눅스 운영체제를 가진 컴퓨터 세 대가 있을 때, 윈도우에서 작성한 코드를 맥이나 리눅스에서 실행하지 못한다는 이야기입니다.

개발자가 특정 언어(e.g. C, C++, Java, C#)를 통해 코드를 작성하면, 이 코드를 각자의 **운영체제 플랫폼에 맞게 기계어로 번역**해서 보내줘야 합니다.

분명 같은 언어와 같은 내용을 가지고 있는 코드임에도 불구하고, 플랫폼에 따라 따로따로 컴파일을 해야 하니, 여간 번거로운 일이 아닐 수 없습니다.

Java에서는 JVM(Java Virtual Machine) 도입을 통해 이러한 문제를 해결했습니다.

#### 🔥 JVM의 동작 방식

JVM은 Java Virtual Machine의 약자로, Java compiler에 의해 변환된 `Java bytecode`를 각 플랫폼에 맞는 기계어(Machine Language)로 바꾸어주는 역할을 합니다.

_(여기에서 Java bytecode는 `.class` 파일을 이야기합니다.)_

JVM은 JVM이 `설치된 컴퓨터의 기계어`도 알고 있고, Java compiler에 의해 변환된 `Java bytecode`도 알고 있습니다. 

개발자가 Java를 사용해서 코드를 작성한 다음 Java compiler가 `Java bytecode`로 컴파일해서 각 플랫폼에 보내면,

JVM은 이 `Java bytecode`를 읽고 각 플랫폼에서 실행할 수 있는 기계어로 바꿔줍니다.

그래서 Java를 사용하는 개발자들은 JVM이라는 프로그램만 설치해두면, 어떤 언어로 컴파일 해야 할지 전혀 신경쓰지 않아도 되는 것입니다!

#### 🔥 JVM에 Java말고 다른 언어도 올릴 수 있나요?

Java 외에 다른 언어도 JVM에 올릴 수 있습니다.

JVM은 `Java bytecode`를 플랫폼에 맞는 기계어로 바꾸는 일을 합니다.

반대로 생각해보면 `Java bytecode`로 컴파일이 될 수 있는 언어라면 JVM에 올릴 수 있지 않을까요?

네! 맞습니다. Kotlin, Scala, Groovy, Clojure와 같이 `Java bytecode`로 컴파일되는 언어라면 JVM에 올릴 수 있습니다.

안드로이드 앱을 만들거나, 스프링 부트로 프로그래밍할 때 Java 뿐만 아니라 Kotlin도 사용할 수 있는 것이 위와 같은 이유 때문입니다.

---

### ✅ JVM의 장단점

#### 🔥 장점

1️⃣ **platform-independent (플랫폼에 종속적이지 않다)**

JVM을 사용하는 Java의 가장 큰 장점은 `한 번 작성하면, 어디서든 실행할 수 있다 (Write Once, Run Anywhere)`입니다.

이 말은 곧 특정 플랫폼에 종속적이지 않다는 이야기이고, 이는 큰 장점이 됩니다.

C/C++와 같은 경우에는 특정 플랫폼에 맞게 컴파일 되지만, Java는 `bytecode`로 컴파일됩니다. 

JVM을 통해 `bytecode`를 JVM이 설치된 컴퓨터의 OS의 기계어로 변환하기 때문에, JVM을 설치할 수 있는 모든 플랫폼에서 실행될 수 있습니다. 

2️⃣ **Memory management (메모리 관리)**

JVM이 OS에 맞도록 메모리를 관리합니다. C, C++과 달리 Java에서는 생성한 배열의 메모리를 예약하거나, pointer를 조작할 필요가 없습니다. JVM이 모두 관리하기 때문이죠.

변수/객체 생성 과정에서 필요한 메모리 할당, 메모리 엑세스 추적을 통한 GC(Garbage Collectoe) 동작을 통한 메모리 회수과 같은 동작을 모두 관리합니다.

GC 동작으로 인해 성능 저하가 발생할 수 있지만, 개발자 입장에서는 아주 편리해집니다.

개발자는 소프트웨어 개발 시, 메모리를 언제 할당하고 언제 해제해야 할지 고민하지 않아도 됩니다. 또한 C, C++와 같은 언어에서 **휴먼 에러**로 인해 발생할 수 있는 `메모리 누수(memory leak)`가 일어날 가능성이 매우 낮아집니다.

3️⃣ **Security & Verification (보안 & 검증)**

#### 🔥 단점

1️⃣ **Performance (성능 저하)**

JVM에서 실행되는 프로그램은 C/C++처럼 특정 플랫폼에 맞는 native 언어로 작성된 프로그램보다 느립니다.

특정 플랫폼에 맞는 네이티브 언어로 작성된 프로그램은 특정 OS/하드웨어에 최적화되어 있지만, Java bytecode는 platform-independent(플랫폼에 종속적이지 않음)하기 때문에 특정 하드웨어에 최적화된 코드가 아닙니다.

그렇기 때문에 성능에서 차이가 날 수 밖에 없습니다.

JVM 최신 버전에서는 `JIT(Just-In-Time) compiler` 도입을 통해 위와 같은 문제점을 개선했습니다.

`JIT compiler`는 `bytecode`를 네이티브 언어로 컴파일 한 후, 프로그램이 실행되는 동안 어떤 메서드나 코드 블록이 자주 호출되는지 분석합니다. 

자주 사용되는 코드의 경우 **이미 컴파일 된 네이티브 코드**를 캐시에 저장했다가 직접 실행하는 방식을 사용하여 성능 개선을 합니다.

2️⃣ **Memory overhead (메모리 오버헤드)**

JVM은 Java 프로그램을 실행하기 위한 런타임 환경(JRE; Java Runtime Environment)를 제공하는데, 이 환경 자체가 추가적인 메모리를 필요로합니다.

또한 JVM은 `GC(Garbage Collector)`를 통해 메모리를 관리하는데, `GC`가 사용하지 않는 객체를 메모리에서 자동으로 해제해주지만 `GC`가 동작하는 과정에서 JVM의 메모리 한계에 도달해 `OutOfMemoryError`가 발생할 수 있습니다.

`JIT compiler`는 bytecode를 네이티브 코드로 컴파일하여 성능을 최적화하지만, 그 과정에서 메모리가 추가적으로 필요합니다.

3️⃣ **JVM itself (JVM 그 자체)**

JVM 그 자체가 문제가 될 수 있습니다.

Java 프로그램을 실행하기 위해서는 JVM에 의존하게 되는데, 만일 JVM에 문제가 발생한다면 프로그램 코드에 문제가 없음에도 불구하고 오류가 발생할 수 있습니다.

물론 JVM에 오류가 일어날 가능성은 매우 적지만, 그 가능성이 0는 아닙니다.

---

### ✅  참고 자료 & 링크

- [자바를 알아보자(+JVM, JRE, JDK의 정체)](https://www.youtube.com/watch?v=OxvtGYvVkRU)

- [Java compiler - Wikipedia](https://en.wikipedia.org/wiki/Java_compiler)

- [JVM vs JRE vs JDK: What's the Difference? | IBM](https://www.ibm.com/think/topics/jvm-vs-jre-vs-jdk)