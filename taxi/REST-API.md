# REST TAXI API

# Требования
Спроектировать API для Яндекс Такси (REST):
- рассчитать время и стоимость маршрута (со звездочкой еще и разные тарифы);
- сделать заказ такси по выбранному маршруту (со звездочкой еще и разные пути);
- посмотреть профиль водителя и клиента
- узнать статус загруженности водителей
- посмотреть историю поездок
- оставить отзыв о поездке
- изменить свои данные

## Rest

### Рассчитать время и стоимость маршрута:
```json
Endpoint: POST /route/calculate
Request Body: {
  "start_location": "string", // начальное местоположение
  "end_location": "string", // конечное местоположение
  "tariff": "string" // тариф
}
Response Body: {
  "duration": "string", // продолжительность маршрута
  "price": "string" // стоимость маршрута
}
```

### Сделать заказ такси по выбранному маршруту:
```json
Endpoint: POST /order
Request Body: {
  "start_location": "string", // начальное местоположение
  "end_location": "string", // конечное местоположение
  "tariff": "string" // тариф
}
Response Body: {
  "order_id": "string", // идентификатор заказа
  "price": "string", // стоимость заказа
  "driver_name": "string", // имя водителя
  "driver_phone": "string", // телефон водителя
  "car_model": "string", // модель машины
  "car_number": "string" // номер машины
}
```

### Посмотреть профиль водителя и клиента:
```json
Endpoint: GET /profile
Request Body: {}
Response Body: {
  "user_type": "string", // тип пользователя (водитель/клиент)
  "name": "string", // имя
  "phone": "string" // телефон
}
```

### Узнать статус загруженности водителей:
```json
Endpoint: GET /drivers/status
Request Body: {}
Response Body: {
  "busy_drivers": "int", // количество занятых водителей
  "free_drivers": "int" // количество свободных водителей
}
```

### Посмотреть историю поездок:
```json
Endpoint: GET /trips
Request Body: {}
Response Body: [
  {
    "start_location": "string", // начальное местоположение
    "end_location": "string", // конечное местоположение
    "price": "string", // стоимость
    "date": "string" // дата поездки
  }
]
```

### Оставить отзыв о поездке:
```json
Endpoint: POST /trips/{trip_id}/review
Request Body: {
  "rating": "int", // оценка поездки
  "comment": "string" // комментарий
}
Response Body: {}
Изменить свои данные:
css
Endpoint: PUT /profile
Request Body: {
  "name": "string", // имя
  "phone": "string" // телефон
}
Response Body: {}
```

### Изменить свои данные:

``` json
Endpoint: PUT /profile
Request Body: {
  "name": "string", // имя
  "phone": "string" // телефон
}
Response Body: {}
```