# social 로그인 할때 application.yml 주의 사항

## github, facebook만 social login을 하겠다.

```
compile group: 'org.springframework.security', name: 'spring-security-oauth2-client', version: "${oauth2ClientVersion}"
```

## google, github, facebook social login을 하겠다.

```
compile group: 'org.springframework.security', name: 'spring-security-oauth2-client', version: "${oauth2ClientVersion}"
compile group: 'org.springframework.security', name: 'spring-security-oauth2-jose', version: "${joseVersion}"
```

## facebook에서 email 정보를 가지고 와야 할경우 
- default user-info-uri를 변경해야 한다.
- 해당 방법은 [Spring Security 5 Configuring Custom Provider Properties](https://docs.spring.io/spring-security/site/docs/5.0.3.RELEASE/reference/htmlsingle/#jc-oauth2login-custom-provider-properties)에 나옵니다.

해당 방법을 사용하면 `application.yml`에 아래와 같이 입력하면 됩니다.

```yml
   facebook:
      client-id: {clien-id}
      client-secret: {client-secret}
provider:
   facebook:
       user-info-uri: https://graph.facebook.com/v2.12/me?fields=email,name
```

