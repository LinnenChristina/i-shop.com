# PATCH/profiles/{profil-id}
## Описание
Авторизованный пользователь редактирует данные в профиле.

## Тело запроса
```
{
  "First_name": "Липская",
  "Last_name": "Кристина",
  "Middle_name": "Анатольевна",
  "Phone": "+375291234567",
  "Discount_card_number": 3049447,
  "Date_of_birth": "1985-04-23",
  "Gender": "женский",
  "Delivery_address": "г.Минск ул. Кульман д. 35А кв.202"
}
```
## Тело ответа
```
{
  "message": "Изменения сохранены",
  "profil-id": 123
}
```
## Описание ошибок
400:Некорректный ввод<br>
401:Для изменения данных необходимо пройти аутентификацию<br>
403:У вас нет разрешения на выполнение этого действия<br>
404:Данные не могут быть изменены
