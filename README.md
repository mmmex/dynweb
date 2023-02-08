## Динамический web

Задачи:

- [X] nginx + php-fpm (laravel/wordpress) + python (flask/django) + js(react/angular);
- [ ] nginx + java (tomcat/jetty/netty) + go + ruby;
- [ ] можно свои комбинации.

Реализации на выбор:
- [ ] на хостовой системе через конфиги в /etc;
- [X] [деплой через docker-compose.](/project/docker-compose.yml)

К сдаче принимается:
- [X] vagrant стэнд с проброшенными на локалхост портами
- [X] каждый порт на свой сайт
- [X] [через нжинкс](/project/nginx-conf/nginx.conf)
- [X] Формат сдачи ДЗ - [vagrant](/Vagrantfile) + [ansible](/provision.yml)

---

### Запуск проекта

1. Клонируем репозиторий: `git clone https://github.com/mmmex/dynweb.git`
2. Выполнить вход в папку: `cd dynweb`
3. Выполнить старт проекта: `vagrant up`

Будет запущена 1 ВМ на ubuntu 20.04 в которой будет доступно 3 ресурса с хостовой машины:

Сервис    | Адрес URL
----------|----------------------
django    | http://localhost:8081
nodejs    | http://localhost:8082
wordpress | http://localhost:8083

4. Командой `docker-compose ps` можем увидеть запущенные контейнеры:

```bash
vagrant@DynamicWeb:~/project$ docker-compose ps
  Name                 Command               State                                                                  Ports                                                                
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
app         gunicorn --workers=2 --bin ...   Up                                                                                                                                          
database    docker-entrypoint.sh --def ...   Up      3306/tcp, 33060/tcp                                                                                                                 
nginx       nginx -g daemon off;             Up      80/tcp, 0.0.0.0:8081->8081/tcp,:::8081->8081/tcp, 0.0.0.0:8082->8082/tcp,:::8082->8082/tcp, 0.0.0.0:8083->8083/tcp,:::8083->8083/tcp
node        docker-entrypoint.sh node  ...   Up                                                                                                                                          
wordpress   docker-entrypoint.sh php-fpm     Up      9000/tcp
```