# Homework №7 Sergey Chachanagov

Реализована идемпотентность создания заказа на основе проверки версии.


При размещении заказа проверяется наличие существующих по ID клиента и сумме заказа.
Если такой заказ уже есть и версия нового заказа <= версии существующего,
то возвращается ID существующего заказа. Новый заказ при этом не создается.

## Теоретическая часть.
### Варианты взаимодействий:
1. Только HTTP взаимодействие
   
   ![alt text](scheme1.png)
   
2. Событийное взаимодействие с использованием брокера сообщений для уведомлений
   
   ![alt text](scheme2.png)
   
3. Event Collaboration
   
   ![alt text](scheme3.png)

Вариант, который мне кажется наиболее правильным для решения данной задачи:

№2. Событийное взаимодействие с использованием брокера сообщений для уведомлений



## Практическая часть
Схема приложения:

![alt text](scheme4.png)

Выше приведена схема взаимодействия сервисов.
Аутентификация реализована с использованием forward-auth на Ingress-NGINX.
Пользователю предоставляется REST API.
Межсервисное взаимодействие используется комбинированного вида:
ORDER взаимодействует с BILLING по REST, а с NOTIFICATION асинхронно с помощью Kafka.
***
Установка приложений в неймспейс order-app

```
helm install app app-chart/ --namespace crud-app --create-namespace
helm install auth auth-chart/ --namespace crud-app
helm install billing billing-chart/ --namespace crud-app
helm install cart cart-chart/ --namespace crud-app
helm install catalog catalog-chart/ --namespace crud-app
helm install delivery delivery-chart/ --namespace crud-app
helm install notification notification-chart/ --namespace crud-app
helm install order order-chart/ --namespace crud-app
helm install return return-chart/ --namespace crud-app
helm install warehouse warehouse-chart/ --namespace crud-app
```
***
Коллекция постмана - **"Chachanagov-hm7.postman_collection.json"**

Команда для запуска:
```
newman run Chachanagov-hm7.postman_collection.json
```


helm install app app-chart/ --namespace crud-app --create-namespace
helm install order order-chart/ --namespace crud-app

helm install cart cart-chart/ --namespace crud-app
helm install warehouse warehouse-chart/ --namespace crud-app
helm install auth auth-chart/ --namespace crud-app
helm install billing billing-chart/ --namespace crud-app

helm install catalog catalog-chart/ --namespace crud-app
helm install delivery delivery-chart/ --namespace crud-app
helm install notification notification-chart/ --namespace crud-app
helm install return return-chart/ --namespace crud-app

helm uninstall app --namespace crud-app
helm uninstall order --namespace crud-app

helm uninstall cart  --namespace crud-app
helm uninstall warehouse --namespace crud-app
helm uninstall auth --namespace crud-app
helm uninstall billing --namespace crud-app

helm uninstall catalog --namespace crud-app
helm uninstall delivery --namespace crud-app
helm uninstall notification --namespace crud-app
helm uninstall return --namespace crud-app


docker build --build-arg JAR_FILE=build/libs/*.jar -t temperror/otus-chachanagov-hm:project-return .
docker push temperror/otus-chachanagov-hm:project-return



cat /bitnami/rabbitmq/conf/rabbitmq.conf
rabbitmqctl authenticate_user someuser somepassword