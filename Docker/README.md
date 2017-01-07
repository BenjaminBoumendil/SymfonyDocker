1 : Create Docker images
-----------------------------

In Docker directory, run the commands :
```bash
$ docker build -t ben/apache ./apache/
$ docker build -t ben/php-fpm:7.0 ./php-fpm7.0/
$ docker build -t ben/data_application ./data_application/
$ docker build -t ben/data_sql ./data_sql/
$ docker build -t ben/sql ./sql/
$ docker build -t ben/phpmyadmin ./phpmyadmin/
```

2 : Modify docker-compose.yml
-----------------------------
You must modify volumes for `test_application` and `test_data` containers with your own directory, for example :
```yaml
test_application:
    image: ben/data_application
    volumes:
        - /home/Test-Docker-Sf/Symfony:/var/www/html
test_data:
    image: ben/data_mysql
    volumes:
        - /home/Test-Docker-Sf/Data:/var/lib/mysql
```

3 : Run the application
-----------------------------

In Symfony directory, run the command :
```bash
$ docker-compose up -d
```

To get `ben/apache_php` container ID, run the command :
```bash
$ docker ps
```

With the ID, you can use composer to download vendors :
```bash
$ docker exec <ID> composer install
```

4 : Test the application
-----------------------------
Symfony application : [http://localhost:60000/app_dev.php](http://localhost:60000/app_dev.php)

PHPMyAdmin : [http://localhost:60002](http://localhost:60002)

MySQL : [http://localhost:60001](http://localhost:60001)

5 : Stop the application
-----------------------------
In Symfony directory, run the command :
```bash
$ docker-compose stop
```
