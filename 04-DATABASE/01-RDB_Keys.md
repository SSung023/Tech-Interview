
### ✅ Database Key란?

Database key란 Table 간의 관계(Relationships)를 이루고, 데이터 무결성을 보장하기 위해 사용되는 태그(Tag)같은 존재입니다.

Key는 Table에서 원하는 레코드(row)를 검색하고 식별하기 위해 꼭 필요하며, 제일 많이 사용되는 Key의 타입은 `PK(Primary Key)`와 `FK(Foreign Key)` 입니다.

Database key는 다음과 같은 장점이 있습니다. 

-   **Unqiue Identification**  
                                  key의 제일 큰 역할은 테이블 내에 있는 각각의 레코드들을 식별하는 것입니다. _주민등록증_과 같은 역할을 하며, 두 개 이상의 레코드가 중복된 값을 가지지 않아야 합니다.
-   **Data Integrity**  
    Key는 데이터의 정확성(accuracy)와 지속성(consistency)를 유지할 수 있도록 합니다. _유일성(uniqueness)_를 유지함으로서, 레코드의 중복을 방지하고, 각 레코드가 다른 값을 갖는 것을 보장할 수 있습니다.
-   **Efficient Data Retrieval**  
    Key는 테이블에서 `indexing system` 역할을 합니다. 특정 데이터를 얻기 위해 데이터베이스에서 쿼리를 요청했을 때 key를 이용하여 적절한 row의 위치를 빠르게 찾을 수 있고, 이를 통해 검색 속도와 효율성이 크게 증가할 수 있습니다.

---

### ✅ Primary Key(PK): 기본 키

`Primary Key(이하 PK)`는 candidate key에서 선택된 키로서, `PK`를 통해 테이블에서 각 레코드들을 unique하게 구분할 수 있습니다. 

RDB(Relational database system)에서 `PK`는 `FK(Foreign Key)`를 통해 테이블을 서로 연결시키는 중요한 역할을 합니다.

PK는 다음과 같은 특징을 가지고 있습니다.

1.  **Only one per table**  
    한 테이블에는 오직 하나의 PK만 존재할 수 있습니다.
2.  **Unique**  
    한 테이블에 저장되어 있는 레코드들의 PK는 모두 다른 값을 가지고 있어야 합니다. (중복 허용 X)
3.  **Not Null**  
    각 레코드들은 모두 PK를 가지고 있어야 하며, `NULL`이 아니어야 합니다.
4.  **Unchanging**  
    레코드가 저장될 때 한 번 설정된 PK는 계속 바뀌지 않아야 합니다.

---

### ✅ Cancidate Key: 후보 키

`cancidate key(후보 키)`는 하나 이상의 column들의 조합으로 만들 수 있는 unique한 조합입니다. 이를 통해 Table 내에 있는 레코드들을 구별할 수 있으며, 이들 중에서 `PK(Primary Key)`가 될 수 있습니다.

`PK`가 될 수 있는 후보들이기 때문에 `candidate key`라고 불립니다. 

`candidate key`에 포함되는 column들의 값(혹은 조합)은 다른 레코드에 없어야 합니다.

예를 들어 `User` 테이블이 있고, `user_id`, `first_name`, `last_name`, `date_of_birth` 컬럼이 있다고 가정해봅시다.

가능한 `candidate key`은 `user_id`, 그리고 `first_name과 `last_name`의 조합입니다. 

이 때, `user_id`는 모든 레코드가 각자 다른 값을 가지고 있어야 합니다.

`first_name`과 `last_name` 각각의 값은 다른 레코드에도 동일한 값이 있을 수 있지만, 두 값 모두 같은 레코드는 없어야 합니다.

---

### ✅ Unique Key

`unique key`의 제약조건(constraint)은 테이블에 있는 하나의 column 또는 여러 column들의 조합이 unique해야 한다는 것 입니다.

`PK`와 유사하게 `unique key`는 유일성(uniqueness)를 보장하지만, **NULL을 허용**합니다.

SQL문을 통해 Table을 생성할 때 `UNIQUE` 제약을 설정함으로서 `unique key`를 설정할 수 있으며, 이를 통해 column들의 중복된 값이 들어가는 것을 막을 수 있습니다.

밑과 같이 table을 생성할 때 `NOT NULL UNIQUE` 옵션을 통해 특정 column에 `unique` 제약 조건을 설정할 수 있습니다.

```
CREATE TABLE Users (
  UserID INT PRIMARY KEY,
  Email VARCHAR(50) NOT NULL UNIQUE,  -- Email is unique and NOT NULL
  FirstName VARCHAR(50) NOT NULL,
  LastName VARCHAR(50) NOT NULL,
  ... (other user attributes)
);
```

---

### ✅ Foreign Key(FK): 외래 키

`foreign key(이하 FK)`는 `unique key` 또는 `PK`를 통해 다른 테이블과의 관계(relationship)을 만드는 column입니다.

`FK` 컬럼은 참조하고자하는 `PK` 혹은 `unique key`의 값과 일치해야 합니다. 

이를 통해 relational database를 구성할 수 있으며, 여러 테이블에 흩어져 있는 데이터들을 연결하고, 쿼리를 요청할 수 있게 됩니다.

예를 들어 쇼핑몰 서비스에서 고객의 정보를 저장하는`Customers` 테이블과 주문 정보를 저장하는 `Orders` 테이블을 다음과 같이 생성한다고 가정해봅시다.

```
CREATE TABLE Customers (
  customer_id INT PRIMARY KEY,
  first_name VARCHAR(50) NOT NULL,
  last_name VARCHAR(50) NOT NULL,
  ... (other customer attributes)
);

CREATE TABLE Orders (
  order_id INT PRIMARY KEY,
  customer_id INT NOT NULL,
  order_date DATE,
  ... (other order attributes),
  FOREIGN KEY (customer_id) REFERENCES Customers(customer_id)
    ON DELETE RESTRICT
    ON UPDATE CASCADE
);
```

`Orders` 테이블에 있는 `customer_id`는 `Customer` 테이블에 있는 `customer_id`을 참조하는 foreign key입니다.

따라서 `Orders` 테이블에서의 customer_id는 참조하고자하는 `Customers` 테이블의 customer_id와 값이 동일해야 합니다.

---

### ✅ Super Key: 슈퍼 키

`super key`는 테이블 내에서 다른 레코드들과 구분할 수 있는 하나 이상의 column으로 이루어진 조합입니다.

`primary key`를 아우르는 더 큰 개념이며, 고유 식별(unique identification)을 위해 여러 개의 column을 `super key`로 선정할 수 있습니다.

모든 `super key`는 유일성(uniqueness)를 보장하는데, 그렇다고 모든 `super key`가 `PK`가 되는 것은 아닙니다.

`PK`는 레코드를 구분하기 위해 특별하게 선택된 key입니다.

```
CREATE TABLE Users (
  user_id INT PRIMARY KEY,
  first_name VARCHAR(50) NOT NULL,
  last_name VARCHAR(50) NOT NULL,
  ... (other user attributes)
);
```

위와 같이 `Users` 테이블을 생성한다고 했을 때 `super key`에는 어떤 조합이 해당할까요?

`super key`는 여러 개의 column을 조합하여 unique하게 식별할 수 있으면 됩니다.

따라서 `user_id` 뿐만 아니라, `user_id`, `first_name`, `last_name`의 조합 또한 super key로 볼 수 있습니다.

---

### ✅ Alternate Key: 대체 키

`alternate key`는 `candidate key(후보 키)`들 중 `PK`로 선택되지 않은 키입니다.

alternate가 의미하는 바는, 레코드를 unique하게 구분할 수 있지만 식별(identifying)할 목적은 아니라는 뜻입니다.

`alternate key`는 여러 테이블에서 unique 제약사항을 두거나, 다른 테이블에서 각자 다른 column들을 참조할 때 유용합니다.

예를 들어 `Students` 라는 테이블을 다음과 같이 생성한다면 `social_security_number`가 `alternate key`가 될 것입니다.

`student_id`는 PK이므로 이를 제외한 column에서 `social_security_number`가 유일성, 식별성(identification)의 조건을 만족하기 때문입니다.

```
CREATE TABLE Students (
  student_id INT PRIMARY KEY,
  social_security_number VARCHAR(11) UNIQUE, -- Enforce uniqueness for SSN (privacy concerns)
  first_name VARCHAR(50) NOT NULL,
  last_name VARCHAR(50) NOT NULL,
  ... (other student attributes)
);
```

---

### ✅ Composite Key: 복합 키

`composite key`는 테이블에서 2개 이상의 column을 조합하여, 각 레코드를 식별할 수 있도록 하는 key를 이야기합니다.

각각의 column을 보았을 때에는 unique하지 않을 수 있지만, 여러 개의 column을 조합해봤을 때에는 해당 값을 가지는 레코드는 단 하나여야 합니다. (유일해야 함)

아래의 예시를 알아봅시다. 

`Orders` 테이블에서 `OrderID`와 `ProductID`의 조합을 `composite key`로 볼 수 있습니다.

이 둘의 조합은 유일하며, 단 하나의 레코드를 추출할 수 있습니다.

```
CREATE TABLE Orders (
  OrderID INT NOT NULL,
  ProductID INT NOT NULL,
  Quantity INT,
  ... (other order item attributes),
  PRIMARY KEY (OrderID, ProductID) -- Composite primary key
);
```

---

### ✅  참고 자료 & 링크

- [https://www.youtube.com/watch?v=gjcbqZjlXjM](https://www.youtube.com/watch?v=gjcbqZjlXjM)

- [https://inpa.tistory.com/entry/DB-%F0%9F%93%9A-%ED%82%A4KEY-%EC%A2%85%EB%A5%98-%F0%9F%95%B5%EF%B8%8F-%EC%A0%95%EB%A6%AC](https://inpa.tistory.com/entry/DB-%F0%9F%93%9A-%ED%82%A4KEY-%EC%A2%85%EB%A5%98-%F0%9F%95%B5%EF%B8%8F-%EC%A0%95%EB%A6%AC)

- [https://airbyte.com/data-engineering-resources/database-keys](https://airbyte.com/data-engineering-resources/database-keys)