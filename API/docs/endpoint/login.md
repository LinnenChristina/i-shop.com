# POST/auth/login
## Описание
Аутентификация пользователя с использованием логина и пароля.

## Тело запроса и ответа
```
{
  "request": {
    "email": "user123@gmail.com",
    "password": "password123"
},
  "response": {
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpZCI6IjEyMzQiLCJ1c2VybmFtZSI6ImJpcnNjaG5lcnNvZXZfaGVsbG9fc2VjdXJpdHkiLCJyb2xlIjoidXNlciJ9.cZL6FJ2EKzK4gSKpPVo5v6poE1T9m3MxoA3on8RHkJ2I"
}
}
```
