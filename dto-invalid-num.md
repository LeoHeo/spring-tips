## 삽질의 시작
```
public enum Provider {
  GENERAL,
  FACEBOOK,
  GOOGLE
}
```

위와 같은 enum이고 아래같이 invalid한 provider값을 post함
```json
{
	"provider": "test"
}
```

## 원인
- `jsonParseError`라는 에러가 나면서 `@Valid`를 로직을 안타서 `missing required value`라는 에러메세지가 response가 안된다.

```java
@PostMapping("/signup")
public void singup(@Valid @RequestBody UserSaveDto userSaveDto, BindResult result) {
  if (result.hasErrors()) {
    throw new BadRequestException("missing requied value");
  }

  // do somthing..
}
```

## 해결
- enum 클래스에 `@JsonCreator`를 추가

```java
@JsonCreator
public static Provider create(String requestValue) {
  return Stream.of(values())
            .filter(v -> v.toString().equalsIgnoreCase(requestValue))
            .findFirst()
            .orElse(null)
}
```
