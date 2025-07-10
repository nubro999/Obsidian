
네, **JWT 토큰**(JSON Web Token)에 대해 쉽게 설명해드릴게요!

---

# 1. **JWT란?**

- **JWT**는 **JSON Web Token**의 약자로,  
  웹에서 **사용자 인증**과 **정보 전달**에 널리 쓰이는 토큰 기반 인증 방식입니다.
- JWT는 **서버-클라이언트 간에 정보를 안전하게 주고받기 위해** 사용됩니다.
- **토큰**은 "전자 서명된 문자열"로, 위조나 변조를 방지할 수 있습니다.

---

# 2. **JWT 구조**

JWT는 **.**(점)으로 구분된 **3개의 부분**으로 이루어져 있습니다.

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
.
eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ
.
SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

각 부분은 다음과 같습니다:

| 부분      | 내용(예시)                        | 설명                                      |
|----------|-----------------------------------|-------------------------------------------|
| Header   | eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9 | 토큰 타입, 서명 알고리즘 정보              |
| Payload  | eyJzdWIiOiIxMjM0NTY3ODkw...        | 실제 데이터(Claims, 사용자 정보 등)         |
| Signature| SflKxwRJSMeKKF2QT4fwpMeJf36...     | 서명(위조 방지, 비밀키로 생성)             |

---

## **각 부분의 역할**

1. **Header**
   - 토큰의 타입(JWT)과 서명에 사용된 알고리즘(예: HS256) 정보를 담음
2. **Payload**
   - 실제 데이터(Claims)를 담음
   - 예시: 사용자 ID, 만료 시간, 이메일 등
3. **Signature**
   - Header와 Payload를 비밀키로 서명해서 위조를 막음

---

# 3. **JWT의 동작 원리**

1. **로그인 성공 시 서버가 JWT 생성**
2. **클라이언트(브라우저/앱)가 JWT를 저장(일반적으로 LocalStorage, 쿠키 등)**
3. **이후 요청마다 JWT를 Authorization 헤더에 담아 서버로 전송**
4. **서버는 JWT의 서명을 검증하여 신뢰할 수 있는 요청인지 확인**

---

# 4. **JWT의 장점**

- **Stateless**: 서버가 세션을 따로 저장하지 않아도 됨 (확장성↑)
- **간편한 정보 전달**: 토큰 안에 필요한 정보를 담아 전송 가능
- **다양한 플랫폼에서 사용 가능**: 웹, 모바일, 서버 등

---

# 5. **JWT의 단점/주의점**

- **Payload는 암호화되지 않음**: Base64Url 인코딩만 되어 있으므로, 민감한 정보는 넣지 말 것
- **토큰 탈취 시 위험**: 토큰이 유출되면 누구나 인증된 것처럼 행동할 수 있음(HTTPS 필수)
- **만료 후 갱신(Refresh Token) 로직 필요**

---

# 6. **실제 예시 (JWT Payload 예시)**

```json
{
  "sub": "1234567890",    // 사용자 ID
  "name": "John Doe",     // 사용자 이름
  "iat": 1516239022,      // 발급 시간(Unix timestamp)
  "exp": 1516242622       // 만료 시간(Unix timestamp)
}
```

---

# 7. **JWT의 사용 예시 (HTTP 헤더)**

```
Authorization: Bearer <JWT 토큰>
```

---

# 8. **정리**

- **JWT**는 인증 및 정보 전달을 위한 안전한 토큰 시스템입니다.
- 서버-클라이언트 간에 **서버 상태를 저장하지 않고** 인증이 가능하게 해줍니다.
- 토큰 자체에 정보와 서명이 포함되어 있어 **위조 방지**가 가능합니다.

---

**더 궁금한 점**  
- JWT 생성/검증 코드 예시  
- JWT와 세션의 차이  
- Refresh Token의 개념  
- 안드로이드/스프링에서 JWT 적용법  
등이 궁금하다면 언제든 질문해 주세요!