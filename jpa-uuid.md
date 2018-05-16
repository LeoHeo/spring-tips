## JPA ID IDENTITY 전략

```java
@Entity
@Table(name = "ORDERS")
public class Order {

  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  private Long id;
  private String item;
}
```

- 위와 같이 IDENTITY 전략을 사용할 경우 id 값은 1씩 차근 차근 올라간다.
- 하지만 DB Sharding을 할 경우 A DB 1부터 증가, B DB 1부터 증가 이럴경우 id가 unique하지 않는다.
- 그렇지 않을경우 `고유번호를 생성하는 작업` 하는 채번 테이블이 존재해야 한다.

## JPA ID uuid 전략
- Hibernate에서는 [UUIDGenerator](https://github.com/hibernate/hibernate-orm/blob/9b00aaf9a55f9879a512b34c13dd25425264494b/hibernate-core/src/main/java/org/hibernate/id/factory/internal/DefaultIdentifierGeneratorFactory.java#L64)를 제공한다.
- UUIDGenerator를 이용해서 Entity를 만들면 아래와 같다.

```java
@Entity
@Table(name = "ORDERS")
public order {

  @Id
  @GeneratedValue(generator = "uuid2")
  @GenericGenerator(name = "uuid2", strategy = "uuid2")
  @Column(columnDefinition = "BINARY(16)")
  private UUID id;
  private String item;
}
```

## UUIDGenerator 설명
- UUIDGenerator는 아래와 같이 5개의 영역으로 UUID를 생성한다.

```
bd5ea7dc-f0cf-41a6-b103-a8e6774971a3
{time_based}-{DCE based using POSIX UIDs}-{name based (md5 hash)}-{random numbers based}-{name based (sha-1 hash)}
```

- [각각 영역에 대한 설명](https://github.com/hibernate/hibernate-orm/blob/9b00aaf9a55f9879a512b34c13dd25425264494b/hibernate-core/src/main/java/org/hibernate/id/UUIDGenerationStrategy.java#L21-L28)은 `UUIDGenerationStrategy`에 적혀있다.

```java
* Which variant, according to IETF RFC 4122, of UUID does this strategy generate?  RFC 4122 defines
* 5 variants (though it only describes algorithms to generate 4):<ul>
* <li>1 = time based</li>
* <li>2 = DCE based using POSIX UIDs</li>
* <li>3 = name based (md5 hash)</li>
* <li>4 = random numbers based</li>
* <li>5 = name based (sha-1 hash)</li>
* </ul>
```