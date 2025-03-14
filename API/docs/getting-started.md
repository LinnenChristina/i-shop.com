# Установка и настройка API

## Как подключиться к API
Для подключения к API вы можете использовать инструменты, такие как [Postman](https://www.postman.com/) или `curl`. 

### Требования для работы с API:
- Токен аутентификации (JWT) требуется для защищённых запросов.
- Доступ к базовым URL серверам API.

## Базовые URL сервера:
- `https://app.swaggerhub.com/apis/KristinaLipskaya/home_i-shop_api/1.0.0#/`

---

## Пример запроса для тестирования

Для тестирования API можно использовать следующий `curl`-запрос:

```bash
curl -X POST "https://app.swaggerhub.com/apis/KristinaLipskaya/home_i-shop_api/1.0.0#/users/post_auth_login" \
-H "Content-Type: application/json" \
-d '{
  "email": "user123@gmail.com",
  "password": "password123"
}'
