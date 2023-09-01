# 1장 JPA 소개

* [1.1 SQL을 직접 다룰 때 발생하는 문제점](#11-sql을-직접-다룰-때-발생하는-문제점)
* [1.2 패러다임의 불일치](#12-패러다임의-불일치)
* [1.3 JPA란 무엇인가](#13-jpa란-무엇인가)


## 1.1 SQL을 직접 다룰 때 발생하는 문제점
자바 어플리케이션에서 데이터베이스의 데이터를 관리하기 위해선 JDBC API를 사용해 SQL을 데이터베이스에 전달한다.

JPA 활용 없이 SQL을 직접 다룬다면,
1. 필요한 데이터를 얻기 위한 SQL을 직접 작성해야 하며,
2. 조회 결과를 직접 객체에 매핑해야 한다.

## 1.2 패러다임의 불일치
> 객체와 관계형 데이터베이스는 지향하는 목적이 서로 다르므로 둘의 기능과 표현 방법도 다르다. 이것을 객체와 관계형 데이터베이스의 <u>패러다임 불일치 문제</u>라 한다.

**상속, 연관관계, 객체 그래프 탐색, 비교**의 경우 객체에서 데이터베이스로 저장할 데이터의 형태로 전환하는 과정에서 추가적인 코드를 작성하는 비용이 추가된다.

### 1.2.1 상속
자식 클래스의 객체를 데이터베이스에 저장하고자 할 때, 객체의 내용을 분해해 부모 클래스의 테이블과 자식 클래스의 테이블로 나누어 저장한다.<br>
또한 조회하는 경우에도 자식 클래스를 조회하고자 한다면, 부모 클래스와 자식 클래스의 테이블들을 조인하고 조회하여 자식 클래스 객체를 생성해야 한다.

### 1.2.2 연관관계
***객체***는 **참조**를 사용해서 다른 객체와 연관관계를 가지고 **참조에 접근해서 연관된 객체를 조회**한다. 반면에 ***테이블***은 **외래 키**를 사용해서 다른 테이블과 연관관계를 가지고 **조인을 사용해서 연관된 테이블을 조회**한다.

```java
class Member {
		Team team;
		
        ...

		Team getTeam() {
				return team;
		}
}

class Team {
		...
}

member.getTeam(); // member 객체에서 team 객체 접근
```

### 1.2.3 객체 그래프 탐색
SQL을 직접 다루면 처음 실행하는 SQL에 따라 객체 그래프를 어디까지 탐색할 수 있는지 정해진다. <br>
한 객체에 연결된 모든 객체 그래프를 전부 불러와 메모리에 올리는 것은 매우 비효율적인 방안이므로, DAO 객체에 상황별 메소드를 여러개 생성해야 한다.

```java
// 처음 조회 시점에서 SELECT MEMBER SQL
Member member = jpa.find(Member.class, memberId);

Order order = member.getOrder();
order.getOrderDate(); // Order 객체를 사용하는 시점에서 SELECT ORDER SQL
```
그러나 JPA 환경에서는 **지연 로딩**이라는 개념을 지원하여 위 예시코드와 같이 연결된 객체가 조회를 시작하는 시점에 SELECT SQL을 실행할 수 있게한다. <br>
만약 `Member` 객체를 사용할 때 마다 `Order` 객체 역시 사용한다면, 지연 로딩을 활용하는 방안 대신 `Member`를 조회하는 시점에서 `Order`를 함께 조회하는 것이 효과적이다.

### 1.2.4 비교
```java
// SQL 직접 활용하여 조회
String memberId = "100";
Member member1 = memberDAO.getMember(memberId);
Member member2 = memberDAO.getMember(memberId);

member1 == member2; // false
```
SQL을 직접 다루는 경우, 기본키 값이 같은 회원 객체를 두 번 조회할 때, 동일성(==)을 비교하면 `false`가 반환된다.
> 자바에서 동일성(==) 비교란 객체 인스턴스의 주소값을 비교한다.

```java
// JPA의 find() 메소드를 활용하여 조회
String memberId = "100";
Member member1 = jpa.find(Member.class, memberId);
Member member2 = jpa.find(Member.class, memberId);

member1 == member2; // true
```
JPA의 `find()` 메소드를 활용하는 경우, 기본키 값이 같은 객체를 여러 번 조회할 때 같은 인스턴스가 반환되는 것을 보장한다.

## 1.3 JPA란 무엇인가?
위에서 설명한 *패러다임 불일치 문제*를 개발자 대신 해결해주는 개념이 **ORM**.

![image](https://github.com/rhyun9584/Today-I-Learned/assets/45452033/a6e538c7-8cd5-45de-b95c-9b2e40a5934f)
![image](https://github.com/rhyun9584/Today-I-Learned/assets/45452033/40598b4f-2614-40b2-bf95-c2f0653d8fd3)


### 1.3.1 JPA 소개
JPA란 자바 ORM 기술에 대한 API 표준 명세이다.

### 1.3.2 왜 JPA를 사용해야 하는가?
1. **생산성**: 지루하고 반복적인 코드 작성을 줄여 생산성을 높일 수 있다.
2. **유지보수**: SQL을 직접 다루게되면, 엔티티에 필드 하나만 추가하여도 직접 수정하거나 추가해야하는 코드의 양이 많다. 이를 JPA가 대신 처리해주므로 유지보수해야 하는 코드의 수가 줄어든다고 볼 수 있다.
3. **패러다임의 불일치 해결**
4. **성능**: 아래 예시처럼, 같은 트랜잭션 안에서 기본키가 같은 회원을 두 번 조회하는 코드를 JPA로 작성한다면 SELECET SQL을 한 번만 데이터베이스에 전달하고 이후에는 이미 조회한 회원 객체를 재사용하여 성능을 향상할 수 있다.
```java
String memberId = "helloId";
Member member1 = jpa.find(memberId);
Member member2 = jpa.find(memberId);
```
5. **데이터 접근 추상화와 벤더 독립성**: 데이터베이스와 어플리케이션 간의 추상화된 데이터 접근 계층을 제공하여 종속되지 않도록 한다. 
6. **표준**: 표준을 사용하면 다른 구현 기술로 손쉽게 변경할 수 있다.
