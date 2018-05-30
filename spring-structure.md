## Spring Boot Structure
- 아래와 같은 structure로 만들자
- [using boot structuring your code](https://docs.spring.io/spring-boot/docs/current/reference/html/using-boot-structuring-your-code.html)

```
com
 +- example
     +- myapplication
         +- Application.java
         |
         +- customer
         |   +- Customer.java
         |   +- CustomerController.java
         |   +- CustomerService.java
         |   +- CustomerRepository.java
         |
         +- order
             +- Order.java
             +- OrderController.java
             +- OrderService.java
             +- OrderRepository.java
```