### ✅ Database 그리고 SQL

\`Database(데이터베이스)\`란 여러 사람이나 프로그램이 데이터를 쉽고 효율적으로 공유하기 위해 체계적으로 관리되는 데이터의 집합을 말합니다.

데이터베이스를 관리하는 시스템을 \`DBMS(Database Management System)\`이라고 이야기하며, 다양한 종류의 DBMS가 있습니다.

데이터베이스의 종류를 나눠보자면 크게 두 가지 유형으로 나뉩니다.

1\. RDB(Relational Database) 관계형 데이터베이스

2\. NoSQL 데이터베이스

이 때, NoSQL은 RDB(관계형 데이터베이스)가 아닌 모든 데이터베이스를 이야기하며 여러 종류가 있을 수 있습니다.

\`SQL\`은 \`Structured Query Language\`의 약자로서, 관계형 데이터베이스(RDB)와 상호작용할 때 사용하는 언어입니다.

---

### ✅ RDB란?

#### 🔥 RDB란?

\`RDB(Relational Database)\`는 데이터를 행(Row)와 열(Column)이 있는 표 형태로 저장을 하는데요, 엑셑(Excel)과 유사한 형태로 생각하시면 됩니다.

관계형 DB는 가장 많이 사용되는 데이터베이스의 유형으로, \`Schema(스키마)\`라는 틀에 맞춰 데이터를 저장합니다.

아래에 있는 테이블을 생성하는 SQL문을 보았을 때, 테이블에 들어갈 데이터의 자료형과 제약사항(constraint)를 모두 명시하고 있는 것을 확인할 수 있습니다.

```
CREATE TABLE `users` (
  `user_id` bigint(20) NOT NULL AUTO_INCREMENT,
  `point` bigint(20) DEFAULT 0,
  `nickname` varchar(20) DEFAULT NULL,
  `information` varchar(100) DEFAULT NULL,
  `tags` varchar(255) DEFAULT NULL,
  `role` enum('NOT_REGISTERED','USER','ADMIN') NOT NULL,
  PRIMARY KEY (`user_id`),
  UNIQUE KEY `UK_2ty1xmrrgtn89xt7kyxx6ta7h` (`nickname`)
);
```

대표적으로 MySQL, MariaDB, PostgreSQL, SQLite, OracleDB 등이 있습니다.

#### 🔥 강점

1️⃣ **데이터의 무결성(Data integrity)**

데이터의 무결성이란 완전하고(complete), 일관되며(consistent), 정확하고(accurate), 믿을 수 있는(trustworthy) 데이터를 이야기합니다.

데이터가 우연하게 또는 의도적으로 변경되거나 파괴되는 상황에 노출되지 않고, 보존되어 데이터를 \`추가, 수정, 삭제\`할 때, 그 연산의 결과가 유효해야 함을 의미합니다.

데이터 무결성에는 크게 세 가지 종류가 있습니다.

1) \`개체 무결성(Entity integrity)\`  
   모든 테이블이 PK(기본키; Primary Key)를 가져야하며, PK는 중복을 허용하지 않아야 하고(unique), 빈 값(Null)을 허용하지 않아야 합니다.

2) \`참조 무결성(Referential integrity)\`  
   FK(외래키; Foreign Key)가 참조하는 테이블의 PK(기본키)와 일치해야 하며, 이를 통해 데이터 간의 일관된 연결을 보장합니다.

3) \`범위 무결성(Domain integrity)\`  
   Column(필드)의 값의 데이터의 범위에 대한 제약 조건(constraint)를 보장한다는 원칙으로, Schema를 통해 정의한 데이터의 타입, 길이, 범위 등의 제약이 보장됩니다.

RDBMS는 \`데이터 무결성\` 유지를 위한 여러 기술적 지원을 도와주고, 그렇기 때문에 개발자는 이러한 제약들을 직접 구현하지 않아도 됩니다.

2️⃣ **명확한 데이터 구조 보장**

RDB의 경우에는 Schema에 맞춰 테이블을 선언하고, 해당 테이블에 데이터를 저장합니다.

Schema라는 틀이 존재하고, 그 틀에 맞춰서 데이터를 저장하기 때문에 명확한 데이터의 구조를 보장합니다.

그 예시로  Schema에 맞춰 밑과 같이 \`users\` 테이블을 생성했을 때, 이후에 \`users\` 테이블에 데이터를 넣을 때에는 그에 맞는 데이터 타입(ex: \`bigint(20)\`)으로 데이터를 삽입해야 하며, 그렇지 않으면 예외가 발생하고 데이터가 저장되지 않습니다.

이를 통해 RDB는 명확한 데이터 구조를 보장합니다.

```
CREATE TABLE `users` (
  `user_id` bigint(20) NOT NULL AUTO_INCREMENT,
  `point` bigint(20) DEFAULT 0,
  `nickname` varchar(20) DEFAULT NULL,
  `information` varchar(100) DEFAULT NULL,
  `tags` varchar(255) DEFAULT NULL,
  `role` enum('NOT_REGISTERED','USER','ADMIN') NOT NULL,
  PRIMARY KEY (`user_id`),
  UNIQUE KEY `UK_2ty1xmrrgtn89xt7kyxx6ta7h` (`nickname`)
);
```

3️⃣ **ACID 특성을 보장한다**

RDB에서는 트랜젝션(Transaction)을 활용하여 \`ACID\` 특성을 보장합니다.

\`ACID\`는 정전, 에러, 기타 다른 사고가 발생해도 데이터베이스에 저장되어 있는 데이터들의 **유효성을 보장**합니다.

#### 🔥 약점

1️⃣ **경직된 Schema**

RDB는 Schema를 정의하고, 거기에 맞춰 테이블을 생성해 데이터를 추가합니다.

만약 새로운 요구사항이 발생하여, Schema가 변경된다면 Column을 추가해줘야 할 것입니다. 이후 요구사항에 맞춰 기능을 개발하다가 신규 기능이 발생하면서 또 Schema가 변경된다면 새로운 Column을 다시 추가해줘야 합니다.

그런데 갑자기 해당 서비스가 엄청난 인기를 끌게 되면서, Schema가 변경되었던 테이블에 엄청나게 많은 데이터(약 5천만개)가 추가되었다고 가정해봅시다.

이 상태에서 Schema가 또 다시 변경되서 Column을 추가하게 된다면, 해당 작업 자체가 많은 위험 부담을 갖는 작업이 될 수 있습니다.

대량의 데이터에 대해서 새로운 Column을 추가해야하기 때문에 상당히 무거운, 위험할 수 있는 작업이 될 수 있습니다.

2️⃣ **과도한 join으로 인한 성능 하락**

RDB는 보통 데이터 중복이 발생하는 것을 지양하는 방향으로 설계하는 것을 권장합니다.

\`정규화(Normalization)\`을 통해 중복되는 데이터는 테이블로 따로 빼내어 저장을 통해 데이터 중복을 피합니다.

따로 빼낸 테이블까지의 데이터까지 모두 조회하고 싶다면 어떻게 해야 할까요?

\`join\`문을 통해 분리되어 있는 테이블의 데이터를 조회할 것입니다. 그런데 만약 **테이블의 수가 엄청나게 많다면** 어떻게 될까요??

통합된 데이터를 읽어오려는 경우, 복잡한 \`join\`을 수행해야 하고, 이는 결국 성능 하락으로 이어질 수 있습니다.

3️⃣ **Scale-out이 쉽지 않음**

DB 서버가 한 대의 컴퓨터에 설치가 되어 있을 때, read/write 요청이 증가하게 되면 DB서버는 부하를 받을 수 밖에 없습니다.

성능이 부족하다는 뜻이죠. 이 경우 어떻게 해야 할까요?  

RDB의 경우 \`Scale-out(수평정 확장)\` 보다 \`Scale-up(수직적 확장)\`을 통해 DB 서버의 성능을 향상시키곤 합니다. 

\`Scale-up\`이란 **하드웨어의 스펙을 업그레이드** 함으로서 성능을 향상시키는 방법을 이야기하고, \`Scale-out\`은 **서버를 추가로 투입**해서 성능을 향상시키는 방법을 이야기합니다.

RDB도 Scale-out(수평적 확장)을 비슷하게 구현할 수 있는데,

DB 서버의 복사본을 만들어놓고(정기적으로 업데이트) → 복사본은 read-only 전용 DB로 사용하게 하는 방법이 있습니다.   
이렇게 하면 \`read\` 연산에 대해서는 트래픽을 분산할 수 있습니다.

하지만 이 방법도 read 트래픽보다 \`write\`트래픽이 압도적으로 많다면 결국 원본 DB 서버가 부하를 받게 되기 때문에 근본적인 해결책이라고는 볼 수 없을 것 같습니다.

RDB는 Transaction을 통해 ACID 특성을 유지하고 서버가 증설되었을 때에도 이러한 특성을 유지해야 하기 때문에, Scale-out(수평적 확장)에는 적절하지 않습니다.

#### 🔥 궁금한 점

RDB의 장점을 검색하다보니 \`RDB는 중복을 최대한 피하기 때문에 update가 빠르다\`는 이야기가 있었습니다.

그런데, 이 이야기를 딱 들었을 때 의문점이 생겼습니다.

_RDB가 중복 데이터를 피하는 것이 update의 성능과 무엇이 관련되어 있는 것일까요?_

NoSQL의 경우 데이터를 빠르게 저장하고 접근할 수 있는데, 그렇다면 update도 NoSQL이 더 빠른거 아닐까요? 빠르게 접근하고 저장이 가능하니 말이죠.

RDB에서 중복을 최대한 피한다는 이야기는 \`정규화(Normalized)\`를 통해 테이블에서 중복되는 내역들을 테이블로 따로 빼내는 등의 작업을 진행하는 것을 이야기합니다.

반면 NoSQL, 대표적으로 _MongoDB_의 경우 데이터를 \`JSON\` 형태로 저장되며, 그렇기 때문에 중복되는 내용들이 생길 수 밖에 없습니다.

예를 들어, 사용자의 주문 정보를 저장하는 \`Orders\` 테이블이 있고,   
1) 주문한 상품의 정보, 2) 주문 수량, 3) 주문한 사용자 정보 와 같은 정보를 저장하고 있다고 가정해보겠습니다.

**RDB**의 경우에는 상품에 대한 정보는 \`Item\` 테이블로, 사용자의 정보는 \`User\` 테이블로 구분한 다음, \`FK(외래키)\`를 통해 서로를 연결합니다.

따라서 총 세 개의 테이블을 통해 정보를 저장하고 있을 것입니다.

**NoSQL**의 경우에는 JSON의 형태로 모든 정보를 저장할 것입니다.

```
{
    itemName: "유자청",
    itemDescribe: "국내산 유자로 만든 유자청입니다.",
    orderedCount: 2,
    orderedAt: "2024-09-24-T12:34:12",
    userName: "HEY"
}
```

그런데 이 때, 상품에 대한 _상세 설명_이 변경되었다고 가정해보겠습니다. 

RDB의 경우에는 \`Item\` 테이블에 저장되어 있던 \`itemDescribe\`만 수정하면 되지만,

NoSQL의 경우에는 모든 데이터들을 확인해서 제품 이름이 "유자청"인 데이터의 모든 상세 설명을 변경해야 할 것입니다.

이러한 점을 미룰어보았을 때, \`update\`를 할 때 RDB가 NoSQL보다 속도가 빠르다는 결론이 나올 수 있습니다.

---

### ✅ NoSQL이란?

#### 🔥 NoSQL이란?

\`Not Only SQL\`의 약자로서, NoSQL은 한 가지 종류의 DB를 뜻하는 것이 아닌 \`Document\`, \`Key-Value\`, \`Graph\`와 같이 SQL이 아닌 모든 DB들의 그룹을 이야기합니다.

RDB에서는 Schema를 통해 데이터의 형태를 엄격하게 지정하는데에 반해, Document DB의 하나인 MongoDB의 경우 어떤 형태로든지 저장이 가능하고, 데이터가 모든 같은 모양일 필요가 없습니다.

또한 RDB와 달리 테이블 간의 관계를 정의하지 않고, 그렇기 때문에 \`join\` 연산이 불가능합니다.

#### 🔥 강점

1️⃣ **유연한 스키마 Flexible Schema**

RDB의 경우에는 Schema에 따라서 테이블을 만들고, 정해진 형태에 따라 데이터를 넣어주어야 합니다.

반면 NoSQL의 경우에는 정해진 Schema가 없습니다. (Flexible Schema)

따라서 기존에 넣었던 데이터와 다른 형태로 넣고 싶으면,

Schema 재정의를 통해 Column을 추가하고 데이터를 넣어야 했던 RDB와는 달리, NoSQL은 데이터를 넣고 싶은 형태로 넣으면 됩니다.

이와 같이 NoSQL은 데이터 구조의 변경 혹은 확장이 일어나도, 추가적인 조치를 취하지 않아도 된다는 장점이 있습니다.

2️⃣ **read(읽기) 속도가 매우 빠르다. (중복 허용)**  
NoSQL의 경우 지정된 엄격한 Schema가 없고, 어플리케이션에서 필요한 형식으로 데이터를 저장하기 때문에 read(읽기) 속도가 빠릅니다.

위에서 RDB와 NoSQL이 데이터를 저장하는 방식의 차이를 이야기했는데요,

RDB는 중복을 지양하기 때문에 테이블이 나눠져 있어 join 연산이 필요했고, NoSQL은 중복을 허용하는 방식으로 데이터를 저장하기 때문에 join 연산을 하지 않는다고 했습니다.

데이터가 대규모로 저장되어 있는 환경을 예로 들어보겠습니다.

RDB의 경우 테이블의 구조에 따라 join 연산을 통해 복잡한 쿼리를 실행하게 될 수 있지만, NoSQL의 경우 join 연산을 수행할 필요가 없기 때문에 읽기 속도의 경우 NoSQL이 더 빠르다고 합니다.

3️⃣ **Scale-out 용이**

NoSQL은 특정 Collection에 모든 데이터가 저장되는 형태로 데이터 중복을 허용합니다. 그렇기 때문에 분산을 할 때에는 단순히 구간만 정해서 자르면 됩니다.

단순하게 데이터가 100개 있다고 가정했을 때 이를 4개의 서버에 분산시켜 저장한다면,

1번 서버에는 1~25, 2번 서버에는 26~50, 3번 서버에는 51~75, 4번 서버에는 76~100 범위의 데이터를 저장하기만 하면 되므로 RDB에 비해서 훨씬 간단하게 분산 저장이 가능합니다.

#### 🔥 약점

1️⃣ **대부분 Transaction을 지원하지 않는다.**

일반적으로 NoSQL에서는 Transaction을 지원하지 않습니다.

RDB에서는 Transaction 지원을 통해 ACID를 보장하지만, 대부분의 NoSQL에서는 Transaction을 지원하지 않기 때문에 ACID를 보장하지 않습니다.

하지만 모든 NoSQL이 Transaction을 지원하지 않는 것은 아닙니다. 대표적으로 \`MongoDB\`의 경우 Transaction을 지원하고, ACID를 일부 보장하는 것을 확인할 수 있습니다.

[https://www.mongodb.com/ko-kr/docs/v5.0/core/transactions/](https://www.mongodb.com/ko-kr/docs/v5.0/core/transactions/)

[트랜잭션 - MongoDB 매뉴얼 v5.0

MongoDB에서 단일 문서에 대한 작업은 원자적으로 이루어집니다. 임베디드 문서와 배열을 사용하면 여러 문서와 컬렉션에 걸쳐 정규화하는 대신 단일 문서 구조에서 데이터 간의 관계를 캡처할

www.mongodb.com](https://www.mongodb.com/ko-kr/docs/v5.0/core/transactions/)

NoSQL에서는 ACID와는 달리 \`BASE\`라는 성질을 가집니다. 이 성질에 대해서는 추가 포스팅을 통해 알아보도록 하겠습니다.

2️⃣ **update의 속도가 느리다.**

위에서 한 차례 이야기했던 내용입니다.

NoSQL의 경우 Schema가 유연하기 때문에 개발자가 저장하고 싶은 형태로 데이터를 저장하게 됩니다.

그에 따라 중복되는 데이터도 자연스레 많아지고, \`update\`문의 속도가 RDB에 비해 상대적으로 느릴 수 밖에 없습니다.

3️⃣ **Schema가 엄격하지 않기 때문에, 데이터 구조 결정이 어렵다. 어플리케이션 단에서 고려해야 한다.**

유연한 Schema를 가지고 있기 때문에 개발자는 데이터를 저장할 때, 서비스의 특성에 맞게 유연하게 저장할 수 있습니다.

하지만 이는 데이터를 불러오거나, 구조를 결정할 때 불편함을 줄 수 있습니다.

그렇기 때문에 개발자는 ERD 설계 단계가 아닌, 어플리케이션 단에서 데이터를 어떻게 저장하고 활용할 것인지 구조를 고려해야 합니다.

---

### ✅ RDB와 NoSQL의 차이점

#### 🔥 그래서 언제 뭘 써야 하는데?

NoSQL은 RDB가 커버하지 못하는 부분들을 보완하기 위해 등장한, 상호 보완적인 존재입니다.

따라서 RDB와 NoSQL 중 하나가 무조건적으로 좋은 것이 아니기 때문에, 개발하려는 서비스의 특성에 맞춰 필요한 데이터베이스를 선택하면 됩니다.

StackOverFlow나 외국 포털사이트를 보면 RDB를 먼저 고려해보고, 서비스의 특성 상 NoSQL을 사용하는 것이 더 좋다고 판단되는 경우 NoSQL을 추가적으로 사용하는 것을 권장하는 것 같습니다.

그러면 어떤 상황에서 어떤 DB를 사용하는 것이 좋을지 정리해보겠습니다.

SQL(RDB)는 다음과 같은 상황에 더 이상적입니다.

1) 높은 수준의 보안과 데이터 무결성이 필요할 때

2) 데이터를 저장하는 구조가 자주 바뀌지 않는 상황

3) 수평적으로 확장할 필요가 없는 상황

4) 자산이나 계좌와 같이 \`Transaction\`을 지원하는 시스템을 개발해야할 때

5) 수평적 확장(Scale-out)이 크게 필요하지 않을 때 

NoSQL은 다음과 같은 상황일 때 더 좋습니다.

1) 높은 수준의 보안이나 데이터 무결성이 딱히 필요하지 않을 때

2) 데이터의 구조가 명확하지 않아 자주 바뀔 것으로 예상되는 상황

3) 유연한 동적 스키마(Schema)가 필요할 때

4) 수평적 확장(Scale-out)이 필요할 때

5) 데이터베이스에 저장되어 있는 데이터를 자주 변경하지 않을 때

#### 🔥 차이점 정리

|   | **SQL** | **NoSQL** |
| --- | --- | --- |
| 종류 | RDB로 단일 종류 | Key-Value, Document, Graph 등 다양한 종류가 있음 |
| Schema | 엄격한 Schema   정해진 데이터 형태로만 저장 가능 | 유연한 Schema   개발자가 필요한대로 저장 가능 |
| update 성능 | SQL의 속도가 더 빠르다 |  |
| read 성능 | NoSQL의 속도가 더 빠르다 |  |
| 특징 | Transaction을 통한 ACID | BASE |
| Join 여부 | 가능 | 불가능 |

---

### 🙋🏻‍♂️ NoSQL을 사용한 경험

팀 프로젝트에서 JWT를 구현했을 때, 보안 조취 중 하나로 Refresh token에 RTR 방식을 적용했습니다.

RTR 전략은 사용자가 Refresh token을 발급받을 때마다 **사용자의 정보**와 **Refresh token의 정보**를 짝지어 DB에 저장(갱신)해놓습니다.

이후 Access token이 만료되고 Refresh token을 통해 토큰을 재발급을 시도할 때 **DB에 저장되어 있는 Refresh token을 대조**하여, 일치할 때에만 토큰을 재발급합니다.

이 때 필요한 기능은 다음과 같았습니다.

1️⃣ 사용자의 정보를 통해 Refresh token의 정보를 조회, 2️⃣ 사용자와 대응되는 Refresh token 정보 저장

Key-Value의 형태로 저장하면 복잡한 구조 없이 간단하게 저장할 수 있고,

NoSQL의 특성 상 사용자가 많아져 데이터가 많아져도 조회(read) 속도가 저하되지 않을 것이라고 판단하여 NoSQL(MongoDB)를 사용했습니다 :)

---

### ✅  참고 자료 & 링크

\- [데이터베이스? SQL? NoSQL? 4분만에 정리해드립니다. - JoCoding](https://youtu.be/IAMdPn3YCG4?si=c9kZnCfVoI_viy4H)

\- [NoSQL 설명!! RDB와는 어떤 차이가 있는지도 설명!! - 쉬운코드](https://www.youtube.com/watch?v=sqVByJ5tbNA)

\- [SQL vs NoSQL 5분컷 설명! - 노마드 코더](https://www.youtube.com/watch?v=Q_9cFgzZr8Q)

\- [\[데이터베이스\] RDB와 NoSQL의 차이는?](https://hyuuny.tistory.com/158)

\- [TTA 정보통신 사전 - 무결성](https://terms.tta.or.kr/dictionary/dictionaryView.do?subject=%EB%AC%B4%EA%B2%B0%EC%84%B1)

\- [데이터 무결성 - 위키백과, 우리 모두의 백과사전](https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%84%B0_%EB%AC%B4%EA%B2%B0%EC%84%B1#:~:text=%EB%8D%B0%EC%9D%B4%ED%84%B0%20%EB%AC%B4%EA%B2%B0%EC%84%B1\(%EC%98%81%EC%96%B4%3A%20data%20integrity,%EC%8B%9C%EC%8A%A4%ED%85%9C%EC%9D%98%20%EC%A4%91%EC%9A%94%ED%95%9C%20%EA%B8%B0%EB%8A%A5%EC%9D%B4%EB%8B%A4.)

\- [SQL vs NoSQL: Full comparison of features, differences](https://www.testgorilla.com/blog/sql-vs-nosql/)

\- [\[DB\] RDB vs NoSQL](https://yummy0102.tistory.com/440)

\- [(논문 번역) SQL vs NoSQL: A Performance Comparison](https://velog.io/@park2348190/%EB%85%BC%EB%AC%B8%EB%B2%88%EC%97%AD-SQL-vs-NoSQL-A-Performance-Comparison)

\- [RDB vs NoSQL](https://velog.io/@sadlthf/RDB-vs-NoSQL)

\- [빅데이터(BigData) 7부 - 수평확장(Scale out)은 RDB보단 NoSQL이지!](https://broccoli45.tistory.com/46)