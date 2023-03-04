# gRPC TAXI API

## Требования
Спроектировать API для Яндекс Такси (gRPC):
- рассчитать время и стоимость маршрута (со звездочкой еще и разные тарифы);
- сделать заказ такси по выбранному маршруту (со звездочкой еще и разные пути);
- посмотреть профиль водителя и клиента
- узнать статус загруженности водителей
- посмотреть историю поездок
- оставить отзыв о поездке
- изменить свои данные

## Пояснение:
Каждый сервис имеет свои методы, принимающие запросы и возвращающие соответствующие ответы в формате protobuf. Для входных запросов используются сообщения, содержащие необходимые данные для выполнения операции. Для выходных ответов используются сообщения, содержащие результаты выполнения операции или ошибки, если таковые возникли.

- `Route`: сервис для рассчета времени и стоимости маршрута;
- `Taxi`: сервис для создания заказа такси;
- `Driver` и `Client`: сервисы для получения профиля водителя и клиента соответственно;
- `DriverLoad`: сервис для получения информации о загруженности водителей;
- `TripHistory`: сервис для получения истории поездок клиента;
- `Review`: сервис для оставления отзыва о поездке;
- `ClientData`: сервис для изменения данных клиента.

## gRPC

```protobuf 
// Рассчитать стоимость и время маршрута
service Route {
  rpc CalculateRoute(RouteRequest) returns (RouteResponse) {}
}

message RouteRequest {
  string origin = 1; // Начальная точка маршрута
  string destination = 2; // Конечная точка маршрута
  int32 tariff_id = 3; // Идентификатор тарифа
}

message RouteResponse {
  int32 duration = 1; // Длительность маршрута в секундах
  int32 price = 2; // Стоимость маршрута в копейках
}

// Сделать заказ такси
service Taxi {
  rpc OrderTaxi(OrderRequest) returns (OrderResponse) {}
}

message OrderRequest {
  string origin = 1; // Начальная точка маршрута
  string destination = 2; // Конечная точка маршрута
  int32 tariff_id = 3; // Идентификатор тарифа
  string path_type = 4; // Тип пути (опционально)
}

message OrderResponse {
  string order_id = 1; // Идентификатор заказа
  int32 price = 2; // Стоимость заказа в копейках
  int32 duration = 3; // Длительность заказа в секундах
}

// Получить профиль водителя
service Driver {
  rpc GetDriverProfile(DriverRequest) returns (DriverResponse) {}
}

message DriverRequest {
  string driver_id = 1; // Идентификатор водителя
}

message DriverResponse {
  string name = 1; // Имя водителя
  string car_model = 2; // Модель автомобиля
  string car_number = 3; // Номер автомобиля
  string rating = 4; // Рейтинг водителя
}

// Получить профиль клиента
service Client {
  rpc GetClientProfile(ClientRequest) returns (ClientResponse) {}
}

message ClientRequest {
  string client_id = 1; // Идентификатор клиента
}

message ClientResponse {
  string name = 1; // Имя клиента
  string email = 2; // Электронная почта клиента
  string phone = 3; // Номер телефона клиента
}

// Получить статус загруженности водителей
service DriverLoad {
  rpc GetDriverLoad(DriverLoadRequest) returns (DriverLoadResponse) {}
}

message DriverLoadRequest {
  string city = 1; // Название города
  string time = 2; // Время (опционально)
}

message DriverLoadResponse {
  int32 load_percentage = 1; // Процент загруженности водителей
}

// Получить историю поездок
service TripHistory {
  rpc GetTripHistory(TripHistoryRequest) returns (TripHistoryResponse) {}
}

message TripHistoryRequest {
  string client_id = 1; // Идентификатор клиента
}

message TripHistoryResponse {
  repeated string trip_id = 1;// список идентификаторов поездок клиента
}

// Оставить отзыв о поездке
service Review {
rpc LeaveReview(ReviewRequest) returns (ReviewResponse) {}
}

message ReviewRequest {
  string trip_id = 1; // Идентификатор поездки
  string text = 2; // Текст отзыва
  int32 rating = 3; // Рейтинг поездки
}

message ReviewResponse {
  bool success = 1; // Флаг успешного оставления отзыва
}

// Изменить данные клиента
service ClientData {
  rpc UpdateClientData(ClientDataRequest) returns (ClientDataResponse) {}
}

message ClientDataRequest {
  string client_id = 1; // Идентификатор клиента
  string name = 2; // Имя клиента (опционально)
  string email = 3; // Электронная почта клиента (опционально)
  string phone = 4; // Номер телефона клиента (опционально)
}

message ClientDataResponse {
  bool success = 1; // Флаг успешного обновления данных клиента
}
```