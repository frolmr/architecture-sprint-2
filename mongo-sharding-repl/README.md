# pymongo-api

## Как запустить

Запускаем mongodb и приложение

```shell
docker compose up -d
```

Инициализируем mongodb и наполняем данными

```shell
./scripts/mongo-init.sh
```

## Как проверить

### Если вы запускаете проект на локальной машине

Откройте в браузере http://localhost:8080

### Если вы запускаете проект на предоставленной виртуальной машине

Узнать белый ip виртуальной машины

```shell
curl --silent http://ifconfig.me
```

Откройте в браузере http://<ip виртуальной машины>:8080

### Проверить шардирование из консоли:

``` shell
docker compose exec -T mongos_router mongosh --port 27020 --quiet
> use somedb;
> db.helloDoc.countDocuments();
> exit();
```

команда вернет кол-во документов в базе (1000)

``` shell
docker exec -it shard1-1 mongosh --port 27021
 > use somedb;
 > db.helloDoc.countDocuments();
 > exit(); 
```
команда вернет кол-во документов в шарде 1-1


``` shell
docker exec -it shard2-1 mongosh --port 27031
 > use somedb;
 > db.helloDoc.countDocuments();
 > exit(); 
```
команда вернет кол-во документов в шарде 2-2

так меняя номера портов (shard1-x: 27021-27023; shrd2-x: 27031-27033) можно убедиться в каждом инстансе реплики одинаковое число записей, при этом сами записи распределены между шардами 


## Доступные эндпоинты

Список доступных эндпоинтов, swagger http://<ip виртуальной машины>:8080/docs
