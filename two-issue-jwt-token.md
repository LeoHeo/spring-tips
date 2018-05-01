# JWT Token을 발급하는 2가지 방법

## io.jsonwebtoken 이용
- `compile group: 'io.jsonwebtoken', name: 'jjwt', version: "${jjwtVersion}"`
- 위에 dependency를 추가하고 아래와 같이 구현한다.
https://github.com/LeoHeo/collect/blob/b1cd389ad7d4d5b21af6cea10dd057831a7dd7f8/src/main/java/com/collect/security/JwtTokenUtil.java#L79-L90

## com.nimbusds.jwt 이용방법
- `compile group: 'org.springframework.security', name: 'spring-security-oauth2-client', version: "${oauth2ClientVersion}"`
- spring-security-oauth2-client안에 `nimbus-jose-jwt`가 있음

## 2가지 방법의 차이점
- [The nimbus-jose-jwt and io.jsonwebtoken - which jjwt library to pick and why?](https://stackoverflow.com/questions/46552922/the-nimbus-jose-jwt-and-io-jsonwebtoken-which-jjwt-library-to-pick-and-why)
