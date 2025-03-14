#Авторизация через Bearer Token (JWT)
##Пример запроса на аутентификацию
Для получения токена аутентификации выполните запрос на эндпоинт /login.
###Пример запроса:
```
curl -X POST "https://app.swaggerhub.com/apis/KristinaLipskaya/home_i-shop_api/1.0.0#/users/post_auth_login" \
-H "Content-Type: application/json" \
-d '{
  "email": "user123@gmail.com",
  "password": "password123"
}'
```
