### ✅ PK

Primary key, PK는 테이블 내의 레코드들을 unique 하게 식별하기 위해 사용되는 key입니다.

다른 레코드들과의 중복 값과 NULL 값을 허용하지 않으며, PK는 FK(외래 키)를 통해 참조되기도 합니다.

지난번 포스팅을 통해 PK에 대해 알아보았는데요, 해당 포스팅에서 PK의 특징에 대해 이야기할 때 `Unchanging`이라고 이야기하며 값이 바뀌지 않아야 한다고 했습니다.

하지만 실제로 데이터베이스에 접속하여 PK의 값을 수정해도, DBMS에서는 'PK는 수정이 불가능합니다'와 같은 문구를 날리지 않습니다. 

수정을 하지 못하게 강제하고 있지 않은거죠.

어떻게 된 일인지, PK는 수정해도 되는 것인지 아닌지 알아보도록 하겠습니다.

---

### ✅ PK 수정이 가능한 조건 

먼저 PK를 수정하는 작업은 다음과 같은 조건을 만족하면 수행 가능합니다.

1️⃣ _변경하고자 하는 값을 지닌 PK가 없는 경우_

2️⃣ _변경하고자 하는 값이 NULL이 아닌 경우_ 

3️⃣ _다른 테이블에서 FK로 사용되고 있지 않은 경우_ 

위의 조건을 만족한 경우 PK 수정이 가능합니다. 하지만 대부분의 경우 PK 수정을 권장하지 않습니다.

---

### ✅ 하지만 PK 수정은 왠만하면 하지말자!

하지만 일반적으로 PK 수정을 피하는 것을 권장합니다. 이유는 다음과 같습니다.

#### 🔥 PK 수정으로 인해 FK에 영향을 미친다

다른 테이블들에서 해당 PK를 FK를 통해 사용하고 있는 경우, PK를 수정하면 FK의 값들까지 모두 수정해야 합니다.

PK 하나를 수정하는 작업이, 많은 테이블들의 레코드들을 수정하는 결과를 낳을 수 있고, 이로 인해 성능 저하가 발생할 수 있습니다. 

#### 🔥 PK 수정으로 인한 index 재정렬 

특별한 설정을 따로 해주지 않는다면, 모든 테이블은 하나의 `Clustered index`를 갖게 됩니다.

`Clustered index`는 PK의 값을 기준으로 물리적으로 정렬이 되어 있는 tree의 구조를 가지고 있습니다. 

이 때, PK에 수정이 일어나면 변경된 값을 바탕으로 **물리적으로 다시 정렬**해야 합니다.

이 또한 무거운 작업이 될 수 있습니다.

#### 🔥 외부와의 참조가 깨질 수 있다

PK는 레코드를 unique하게 식별할 수 있는 용도로 사용되기 때문에, 외부의 시스템(어플리케이션 캐시, 또 다른 DB)와 참조되어 있을 수 있습니다. 

이 때, PK를 수정한다면 이러한 참조가 깨질 수 있고, 이를 위해 별도의 조치가 필요합니다.

#### 🔥 몇몇 RDBMS에서는 `CASCADE UPDATE`를 지원하지 않는다

PK를 수정했을 때 관련되어 있는 FK를 다 같이 수정하는 방법이 있습니다. 바로 `CASCADE UPDATE`입니다.

하지만 Oracle과 같은 몇몇 RDBMS에서는 `CASCADE UPDATE`를 지원하지 않습니다. 

---

### ✅  참고 자료 & 링크

- [database - Can we update primary key values of a table? - Stack Overflow](https://stackoverflow.com/questions/3838414/can-we-update-primary-key-values-of-a-table)

- [Can I change the primary key after a relationship in a database? - Quora](https://www.quora.com/Can-I-change-the-primary-key-after-a-relationship-in-a-database)

- [ORACLE DB - ON UPDATE CASCADE (TRIGGER 사용해서 UPDATE 하기)](https://kimtaehyun98.tistory.com/122)

- [database design - Why would a primary key value change? - Database Administrators Stack Exchange](https://dba.stackexchange.com/questions/140632/why-would-a-primary-key-value-change)