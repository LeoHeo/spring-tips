## 소셜로그인 세션 허용
- 소셜로그인을 사용할 경우 Spring Security에서 세션을 필요할때 사용할 수 있게(이게 default 설정) 헤야 한다.
- `sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS)` 인 경우에는 provider가 넘겨주는 값을 못 가지고 온다.
