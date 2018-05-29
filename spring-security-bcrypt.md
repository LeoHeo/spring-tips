## Spring Security Bcrypt

## password
- n자 이상은 하되 n자 이하는 하지말아라
- n자 이하로 하면 brute force로 빨리 뚫릴수도 있다.

## hashing
- hashing crack하는 방법은 여러가지가 존재한다. 가장 대표적인 2개는 아래와 같다.
- Brute force attack -> 무식하게 모든 경우의 수를 다 시도해본다.
- Rainbow table -> 미리 가능한 패스워드 조합을 다 계산한 테이블을 가지고 비교만 수행하는 것이다. 이것이 dictionary attack인데, 이 dictionary를 해시값 검색에 최적화시킨 것

## 알맞은 hashing
- Rainbow table이랑 Brute force attack를 알아낼 수 없게 비밀번호에는 salt라는걸 쳐야 한다.
- 그중에서 Bcrypt에 대해서 알아보자

## Bcrypt란?
- 애초부터 패스워드 저장을 목적으로 설계
- designed by Niels Provos and David Mazières
- OpenBSD에서 기본 암호 인증 메커니즘으로 사용
- salt가 embedded 포함되어있음 따로 salt를 저장하지 않는다.

```
$2a$10$N9qo8uLOickgx2ZMRZoMyeIjZAgcfl7p92ldGxad68LJZdL17lhWy

$2a - bcrypt_id
$10 -> rounds(cost parameter)
N9qo8uLOickgx2ZMRZoMye - salt
IjZAgcfl7p92ldGxad68LJZdL17lhWy - hash
```

## Sprig Security Bcrypt

### 회원가입
1. 회원가입할때 plaintext + random salt로 암호화 -> encode_password

### 로그인
1. plain text 입력 ssl로 서버 request
2. encode_password에서 [log_rounds 뒤에 128 bit salt를 가져옴(?)](https://github.com/spring-projects/spring-security/blob/b3ca5986791ac5c97022d64646df1a6e1ec2a8b7/crypto/src/main/java/org/springframework/security/crypto/bcrypt/BCrypt.java#L579-L587)
3. plain text + 가져온 128 bit salt로 암호화
4. encode_password 랑 generate_password 비교
5. valid or invalid

## 출처
- [패스워드 보안의 기술](http://www.codeok.net/%ED%8C%A8%EC%8A%A4%EC%9B%8C%EB%93%9C%20%EB%B3%B4%EC%95%88%EC%9D%98%20%EA%B8%B0%EC%88%A0) 