---
description: 구글 로그인 API
---

# 구글 로그인 / 회원가입

#### ‼️ 구글 로그인 플로우

유저의 인가 코드 요청 > 구글 서버에서 해당 유저의 `code` 반환 > 발급받은 `code` 로 유저 정보 Get

(유저 정보: 구글 Access Token, 구글 Refresh Token, Email, 이름 등)

\> 유저 생성 & Astee JWT 발급



## 1. code 발급

### 1) Request

#### Request URL

```javascript
GET /token/google
```

###

### 2) Response

구글 페이지로 요청을 보내어, 설정한 리다이렉트 URI에 유저의 `code` 가 파라미터로 붙어 리다이렉트 된다.

<figure><img src="../.gitbook/assets/스크린샷 2023-03-18 23.21.56.png" alt=""><figcaption></figcaption></figure>

* http://127.0.0.1:8000 -> 추후에 프론트 배포가 완료된다면 프론트 URI로 업로드할 예정
* 해당 URI에서 `code` 파라미터를 가져와, 아래의 요청에서 서버로 전송해주면 됨!

###

## 2. Google Signup/Login

### 1) Request

#### Request URL

```
GET /login/google?code={code}
```

#### Request Parameter

* code: 위에서 발급받은 유저의 code



### 2) Response

```json
{
    "sub": "102728887062895999235",
    "username": "서수경",
    "email": "tjtnrud0967@gmail.com",
    "django_token": {
        "access": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjc5MzIyNDkwLCJpYXQiOjE2NzkxNDk2OTAsImp0aSI6Ijk1YWQwNDQ0YTIzNTRlMmRiNDUyYjIxZTM2OWNhZTU2IiwidXNlcl9pZCI6MX0.oW6iCN4fSk2E1gKOhJrEsL5YVBh7btdccS5O-_g-b3c",
        "refresh": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTY4MTc0MTY5MCwiaWF0IjoxNjc5MTQ5NjkwLCJqdGkiOiI2MTRhMTIyZWVjMzY0YjRkODYzMjc5OWU5YWY5YmE4MiIsInVzZXJfaWQiOjF9.eD5EhZn5c_WPfiqlvnNvQ3LlGj21b51fYxwOIwsJmQI"
    }
}
```

유저 생성 & Django에서 발급한 JWT 토큰 발급



### 3) Status Code

| Status Code | Message     | Description                     |
| ----------- | ----------- | ------------------------------- |
| 200         | OK          | 로그인 성공                          |
| 400         | Bad Request | Invalid Token(code가 유효하지 않은 경우) |
