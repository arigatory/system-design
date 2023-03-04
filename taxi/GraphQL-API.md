# GraphQL TAXI API

## Требования
Спроектировать API для Яндекс Такси (GraphQL):
- рассчитать время и стоимость маршрута (со звездочкой еще и разные тарифы);
- сделать заказ такси по выбранному маршруту (со звездочкой еще и разные пути);
- посмотреть профиль водителя и клиента
- узнать статус загруженности водителей
- посмотреть историю поездок
- оставить отзыв о поездке
- изменить свои данные

## Пояснение:

- `Query`: корневой тип запросов;
- `Mutation`: корневой тип мутаций;
- `Route`: тип для рассчета времени, расстояния и стоимости маршрута;
- `Driver` и Client: типы для получения профиля водителя и клиента соответственно;
- `DriverLoad`: тип для получения информации о загруженности водителей;
- `Trip`: тип для получения информации об истории поездок клиента;
- `Order`: тип для создания заказа такси;
- `Review`: тип для оставления отзыва о поездке.

## GraphQL

```yaml
type Query {
  getRoute(time: Int, distance: Int, tariff: String): Route
  getDriver(driverId: ID!): Driver
  getClient(clientId: ID!): Client
  getDriverLoad: [DriverLoad]
  getTripHistory(clientId: ID!): [Trip]
}

type Mutation {
  createTaxiOrder(route: RouteInput!, path: PathInput!, tariff: String): Order
  leaveReview(tripId: ID!, text: String!, rating: Int!): Review
  updateClientData(clientId: ID!, name: String, email: String, phone: String): Client
}

type Route {
  time: Int
  distance: Int
  price: Float
}

input RouteInput {
  time: Int!
  distance: Int!
  tariff: String
}

input PathInput {
  start: String!
  end: String!
}

type Driver {
  driverId: ID!
  name: String!
  carModel: String!
  carNumber: String!
  rating: Float!
}

type Client {
  clientId: ID!
  name: String
  email: String
  phone: String
}

type DriverLoad {
  driverId: ID!
  load: Int!
}

type Trip {
  tripId: ID!
  date: String!
  driver: Driver!
  route: Route!
  price: Float!
}

type Order {
  orderId: ID!
  driver: Driver!
  route: Route!
  price: Float!
}

type Review {
  success: Boolean!
}
```