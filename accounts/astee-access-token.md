---
description: Astee에서 제공하는 Access Token이 만료된 경우, Refresh Token으로 새 Access Token 요청 API
---

# Astee Access Token 발급



유저가 Astee 접속 > 401 에러 > Refresh Token이 없다면 로그아웃한 유저

유저가 Astee 접속 > 401 에러 > Refresh Token이 있다면 Accee Token 발급

‼️ 유저가 Astee에 접속할 때엔, `Bearer Token` 에 **Access Token**을 담아 요청을 보낸다.



## 1. POST method

### 1) Request

#### Request URL

```javascript
POST /api/token/refresh
```

#### Request Body

```javascript
{
    "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTY1Mjc4MzU4NCwiaWF0IjoxNjUwMTkxNTg0LCJqdGkiOiIwNGYyZWIwYjEzZjQ0MGYwOTA2OTIyMjA1NDQ2Zjk3MCIsInVzZXJfaWQiOjg4fQ.ELTsTpw3ZFVayiKK9y2SEuERzBIiO4YbSOXX8t5iAoE"
}
```

Request Body에 유저의 Refresh Token을 담아 보낸다.

### 2) Response

#### Response body

```json
{
    "access": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjUwMzY0NTg3LCJpYXQiOjE2NTAxOTE1ODQsImp0aSI6IjEwMzgwMmFkNmVlODQ2OWZhYjc2MmE3YmViYjJiYjRhIiwidXNlcl9pZCI6ODh9.V-psXrAdCXE3AgeLv5Bpyas3zDG77v3Ihx708a1lBV8"
}
```



### 3) Status Code

| Status Code | Message      | Description               |
| ----------- | ------------ | ------------------------- |
| 200         | OK           | 새 Access Token 발급 성공      |
| 401         | Unauthorized | Refresh Token이 유효하지 않은 경우 |
