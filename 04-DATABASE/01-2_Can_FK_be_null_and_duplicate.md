### ✅ FK에 대한 궁금증

지난번 포스팅에서 Database의 여러 종류의 Key들을 알아보았다. 

그 중 `Foreign Key, FK`는 다른 테이블의 필드(주로 `Primary Key;PK`)를 참조하여 다른 테이블과의 관계를 맺기 위해 사용되는 키입니다.

`PK`의 경우

1️⃣ NULL을 허용하지 않고,

2️⃣ 레코드들 간의 중복을 허용하지 않는 특징을 갖고 있습니다.

`FK`는 주로 `PK`의 값을 참조하는데, 그렇다면 `FK` 또한 `PK`와 비슷한 성질을 가지고 있을까? 하는 궁금증이 들었습니다.

이번 포스팅에서는 `FK`에도 NULL이 들어갈 수 있는지, 또 중복을 허용하는지 알아보도록 하겠습니다.

---

### ✅ FK는 NULL이 들어갈 수 있으며, 중복을 허용한다.

#### 🔥 NULL이 지니는 의미

`FK`에 NULL값이 들어 갈 수 있는지 알아보지 이전에, 먼저 NULL이 지니는 의미에 대해 먼저 알아보겠습니다.

`NULL`이 의미하는 바는 다음과 같습니다.

1️⃣ 값이 존재하지 않는다

2️⃣ 값이 존재하지만, 아직 그 값이 무엇인지 알지 못한다

3️⃣ 해당 사항과 관련이 없다

#### 🔥 FK에는 NULL이 들어갈 수 있다.

결론부터 이야기를 해보자면, FK에는 NULL이 들어갈 수 있습니다.

위에서 이야기했듯이, FK는 관계를 맺고자하는 테이블의 PK 값을 참조합니다.  반대로 생각해보면 관계를 맺고자하는 테이블의 PK 값이 이미 존재해야 합니다.

이러한 상황에 관계를 맺고자하는 테이블의 레코드가 아직 생성되지 않았다면?

값이 존재하지만(언젠가 값이 추가될 것이지만), 아직 그 값을 알 수 없다는 의미가 됩니다. 따라서 FK에는 NULL이 들어갈 수 있습니다.

예를 들어, `Team` 테이블과 `Users` 테이블이 밑과 같다고 가정해보겠습니다.

```
CREATE TABLE Team (
  team_id INT PRIMARY KEY,
  name VARCHAR(50) NOT NULL,
  ... (other user attributes)
);

CREATE TABLE Users (
  user_id INT PRIMARY KEY,
  FirstName VARCHAR(50) NOT NULL,
  LastName VARCHAR(50) NOT NULL,
  ... (other user attributes),
  FOREIGN KEY (team_id) REFERENCES Team(team_id)
    ON DELETE RESTRICT
    ON UPDATE CASCADE
);
```

`Users` 테이블에는 `team_id`라는 FK를 통해 사용자가 참여한 팀의 정보를 저장합니다.

`Team` 테이블에 5개의 팀의 정보가 이미 존재하는 상태에서, 새로운 참여자가 발생해 사용자의 정보를 저장하려고 합니다.

하지만 사용자는 정보를 등록하면서 팀을 바로 등록하는 것이 아니라, 나중에 팀에 가입하기로 했습니다.

이 경우 Users 테이블에 새로이 저장되는 값은 `(1, gil-dong, hong, null)`이 될 것이며, 이후에 사용자가 팀에 가입하게 되면 null 대신 참여한 팀의 PK가 들어가게 될 것입니다.

#### 🔥 FK는 중복을 허용한다.

결론부터 이야기하자면 FK는 중복을 허용합니다.

위에서 들었던 예시를 보면 여러 사용자가 하나의 팀에 참여할 수 있습니다. 따라서 테이블 간의 관계는 `OneToMany`가 되고, 이 경우에는 당연하게도 FK의 값은 중복이 될 수 밖에 없습니다.

테이블 간의 관계가 `OneToOne`이라면 FK의 값이 unique해질 수 있으며, 이 경우에는 unique constraint(제약 조건)을 통해 유일성을 지키도록 할 수 있습니다.

하지만 기본적으로 FK의 값은 중복을 허용합니다.

---

### ✅  참고 자료 & 링크

- [StackOverFlow - Can a foreign key be NULL and/or duplicate?](https://stackoverflow.com/questions/7573590/can-a-foreign-key-be-null-and-or-duplicate)

- [Foreign keys in referential constraints - IBM](https://www.ibm.com/docs/en/db2-warehouse?topic=constraints-foreign-keys-in-referential)