# Homework №9 Sergey Chachanagov

Реализована распределенная транзакция (Паттерн Сага, реализован с помощью хореографии).

Последовательность действий при совершении заказа:

1. Зарезервировать товар на складе.
2. Списать деньги со счета пользователя.
3. Очистить корзину пользователя.

***
Установка приложений в неймспейс crud-app

```
helm install app app-chart/ --namespace crud-app --create-namespace
helm install order order-chart/ --namespace crud-app
helm install cart cart-chart/ --namespace crud-app
helm install warehouse warehouse-chart/ --namespace crud-app
helm install auth auth-chart/ --namespace crud-app
helm install billing billing-chart/ --namespace crud-app
```
***
Коллекция постмана с тестами - **"Chachanagov-hm9.postman_collection.json"**

Команда для запуска:
```
newman run Chachanagov-hm9.postman_collection.json
```


