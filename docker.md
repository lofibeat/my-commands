```bash

🐳 Docker — контейнеры и образы

## Образы

docker images                   # список локальных образов
docker image ls                 # то же (новый синтаксис)
docker pull image:tag           # скачать образ (например nginx:alpine)
docker build -t name:tag .      # собрать образ из Dockerfile в текущей папке
docker build -f Dockerfile.dev -t app:dev .  # указать другой Dockerfile
docker rmi image                # удалить образ
docker rmi $(docker images -q)  # удалить все образы
docker image prune -a           # удалить неиспользуемые образы

## Контейнеры (запуск и остановка)

docker run image                # запустить контейнер из образа (один раз)
docker run -d image             # запустить в фоне (detached)
docker run --rm image           # удалить контейнер после выхода
docker run -it image sh          # интерактивно с shell (it = stdin + tty)
docker run -p 8080:80 image     # проброс портов хост:контейнер
docker run -v /host/path:/container/path image  # монтировать каталог
docker run -e VAR=value image   # передать переменную окружения
docker run --name mybox image   # задать имя контейнера
docker run --restart unless-stopped image  # перезапускать при падении

docker start container         # запустить существующий контейнер
docker stop container          # остановить контейнер
docker restart container       # перезапустить контейнер
docker kill container          # принудительно завершить
docker pause container         # приостановить (заморозить)
docker unpause container       # возобновить

## Список и информация

docker ps                      # запущенные контейнеры
docker ps -a                   # все контейнеры (включая остановленные)
docker ps -q                   # только ID контейнеров
docker logs container          # вывод логов контейнера
docker logs -f container       # логи в реальном времени (follow)
docker logs --tail 100 container  # последние 100 строк
docker inspect container       # подробная информация (JSON)
docker stats                   # использование CPU/RAM по контейнерам (живой вывод)
docker top container           # процессы внутри контейнера

## Выполнение команд в контейнере

docker exec container command  # выполнить команду в запущенном контейнере
docker exec -it container sh   # интерактивный shell в контейнере (sh или bash)
docker exec -u root container cmd  # выполнить от root
docker exec -e VAR=value container cmd  # с переменной окружения

## Удаление

docker rm container            # удалить остановленный контейнер
docker rm -f container         # удалить принудительно (остановить и удалить)
docker rm $(docker ps -aq)     # удалить все контейнеры
docker container prune         # удалить все остановленные контейнеры

## Docker Compose

docker compose up -d           # запустить сервисы из docker-compose.yml в фоне
docker compose up              # запустить с выводом логов
docker compose down            # остановить и удалить контейнеры
docker compose down -v         # также удалить тома
docker compose ps              # статус сервисов
docker compose logs -f         # логи всех сервисов
docker compose exec service sh # shell в контейнер сервиса
docker compose build           # пересобрать образы
docker compose pull            # скачать образы из compose-файла
docker compose config          # проверить и вывести итоговый конфиг

# Файл: docker-compose.yml (или compose.yaml). Команды выше из каталога с файлом.

## Сети

docker network ls              # список сетей
docker network create mynet    # создать сеть
docker network inspect mynet   # информация о сети
docker run --network mynet image  # запустить контейнер в сети
docker network connect mynet container  # подключить контейнер к сети
docker network rm mynet         # удалить сеть

## Тома (данные)

docker volume ls               # список томов
docker volume create myvol     # создать том
docker run -v myvol:/data image # монтировать том в контейнер
docker volume rm myvol         # удалить том
docker volume prune            # удалить неиспользуемые тома

## Полезные комбинации

docker run -d --name web -p 80:80 -v ./html:/usr/share/nginx/html nginx:alpine
# Запустить nginx в фоне, порт 80, монтировать ./html как контент

docker exec -it $(docker ps -q -f name=web) sh
# Зайти в shell первого контейнера с именем, содержащим "web"

docker system df               # сколько места занимают образы, контейнеры, тома
docker system prune -a         # удалить всё неиспользуемое (образы, контейнеры, сети)
docker system prune -a --volumes  # также удалить неиспользуемые тома
```
