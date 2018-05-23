## @DataJpaTest profile 설정
- Repository를 Test하고자 할때 예를들어 OrderRepository를 테스트한다고 가정해보자. 그러면 아래와 같은 Test class를 만들 것이다.

```java
@RunWith(SpringRunner.class)
@DataJpaTest
public class OrderRepositoryTest {

  @Autowired
  private OrderRepository orderRepository;
}
```

## application.yml datasoure 사용할 경우
- DataJpaTest는 기본적으로 in-memory db로 Test를 진행된다.
- `H2`, `DERBY`, `HSQL` 이렇게 [3종류의 DB](https://github.com/spring-projects/spring-boot/blob/4464a5f5bde9256a46432cfcbe5dd0ba4d34091d/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/jdbc/EmbeddedDatabaseConnection.java#L50-L62)를 사용하며, 아무 설정도 안하면 default는 h2로 돌아간다.
- Test를 돌리게 되면 `jdbc:h2:mem:abcde-22-ddd-aa` 같은 임의의 DB에 값을 넣게 된다.
- `application.yml`에 datasource로 Test를 돌릴려면 `@AutoConfigureTestDatabase(replace = Replace.NONE)`를 설정해야 한다.

```java
@RunWith(SpringRunner.class)
@AutoConfigureTestDatabase(replace = Replace.NONE)
@DataJpaTest
public class OrderRepositoryTest {

  @Autowired
  private OrderRepository orderRepository;
}
```

## 각기 다른 DB 사용해서 Test를 할 경우
- 근데 만약에 `application-test.yml`에 있는 datasource를 끌고올라면 어떻게 해야할까?
- ~이것때문에 좀 삽질을 했지만~ 이럴경우에는 `ActiveProfiles`를 사용하게 된다.

```java
@RunWith(SpringRunner.class)
@AutoConfigureTestDatabase(replace = Replace.NONE)
@ActiveProfiles("test")
@DataJpaTest
public class OrderRepositoryTest {

  @Autowired
  private OrderRepository orderRepository;
}
```

- ActiveProfiles 안에 값은 `application-{profile}.yml` 이다. 
- 이말인 즉슨, ActiveProfiles("mysql")이라면 파일명은 `application-mysql.yml` 이여야 한다는 것이다.
- yml 파일이 있어야 하는 위치는 `test -> resource -> application-{profile}.yml` Hierarchy 구조여야 한다.