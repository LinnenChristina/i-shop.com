# GET/products
## Описание
Получение товаров по ШК в магазине с поддержкой пагинации и сортировки.

## Тело запроса
Нет тела запроса.

## Тело ответа
```
[
  {
    "Product_id": 5614,
    "Product_name": "Природная питьевая негазированная 0,5л",
    "Product_Promotion": "Неделька",
    "Product_Starting_price": 1.2,
    "Discount_Product": 10,
    "Product_Discounted_price": 1.08
  }
]
```
## Описание ошибок
404: Продукт с данным штрихкодом не найден

# DELETE/products/{Product_id}
## Описание
Удаление товара

## Тело запроса
Нет тела запроса.

## Тело ответа
Нет тела запроса. <br>
200: Товар удален

## Описание ошибок
400:Некорректные данные<br>
404:Товар не найден<br>
500:Внутренняя ошибка сервера
