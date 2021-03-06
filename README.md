## Задача 1
- создайте свой репозиторий на https://hub.docker.com;
- выберете любой образ, который содержит веб-сервер Nginx;
- создайте свой fork образа;
- реализуйте функциональность: запуск веб-сервера в фоне с индекс-страницей, содержащей HTML-код 

Файл index.html
```
# cat index.html
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I'm DevOps Engineer!</h1>
</body>
</html>
```
Файл Dockerfile
```
# cat Dockerfile
FROM nginx:1.21.6
COPY index.html /usr/share/nginx/html
```
```
# docker build -t dmitrii1980/mynginx:1.21.6
# docker login
# docker push dmitrii1980/mynginx:1.21.6
```

## Задача 2
Посмотрите на сценарий ниже и ответьте на вопрос: "Подходит ли в этом сценарии использование Docker контейнеров или лучше подойдет виртуальная машина, физическая машина? Может быть возможны разные варианты?"

Детально опишите и обоснуйте свой выбор.

--

Сценарий:

- Высоконагруженное монолитное java веб-приложение; - в этом сценарии можно использовать Docker контейнер, но на физической машине производительность будет выше
- Nodejs веб-приложение; - можно использовать контейнер
- Мобильное приложение c версиями для Android и iOS; - на виртуальной машине, т.к. требуется эмуляция ARM архитектуры
- Шина данных на базе Apache Kafka; - можно использовать контейнер
- Elasticsearch кластер для реализации логирования продуктивного веб-приложения - три ноды elasticsearch, два logstash и две ноды kibana; - на отдельных контейнерах не реализовать, можно с системой оркестрации (swarm/kubernetes). 
- Мониторинг-стек на базе Prometheus и Grafana; - можно использовать контейнеры
- MongoDB, как основное хранилище данных для java-приложения; - базы данных лучше разворачивать на физических хостах или виртуальных машинах. В контейнерах возможно, но не желательно
- Gitlab сервер для реализации CI/CD процессов и приватный (закрытый) Docker Registry. - можно использовать контейнеры

## Задача 3

- Запустите первый контейнер из образа centos c любым тэгом в фоновом режиме, подключив папку /data из текущей рабочей директории на хостовой машине в /data контейнера;
```
# docker run -v /home/vagrant/data:/data -ti centos /bin/bash
```
- Запустите второй контейнер из образа debian в фоновом режиме, подключив папку /data из текущей рабочей директории на хостовой машине в /data контейнера;
```
# docker run -v /home/vagrant/data:/data -ti debian /bin/bash
```
- Подключитесь к первому контейнеру с помощью docker exec и создайте текстовый файл любого содержания в /data;
```
# docker exec -ti fed2e2844a91 /bin/bash
# echo test > /data/file1
```
- Добавьте еще один файл в папку /data на хостовой машине;
```
# echo test > /home/vagrant/data/file2
```
- Подключитесь во второй контейнер и отобразите листинг и содержание файлов в /data контейнера.
```
# docker exec -ti 06229441959e /bin/bash
# ls /data
file1  file2
# cat /data/file1
test
# cat /data/file2
test
```
