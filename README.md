# how to run phpMyAdmin on Debian 11

## try this

run:

```bash
docker compose up --build -d
```

## Post installation

You have to create a user and schema with tables to complete the phpMyAdmin setup:

```bash
docker exec phpmyadmin-phpmyadmin-1 /bin/sh -c 'cat /var/www/html/phpmyadmin/sql/create_tables.sql' > create_tables.sql
docker exec -i phpmyadmin-db-1 mariadb -uroot -proot <create_tables.sql
docker exec -i phpmyadmin-db-1 mariadb -uroot -proot -e "create user phpmyadmin@'%' identified by 'PGRI3cl287WFUfCgWRauoF8Oat1vuJdo'";
docker exec -i phpmyadmin-db-1 mariadb -uroot -proot -e "grant all privileges on phpmyadmin.* to phpmyadmin@'%'";
```

access at http://localhost:8080/phpmyadmin/ with user=root, password=root

## setup summary

On a fresh debian:11 you need:

```bash
apt-get update && apt-get install -y \
    apache2 \
    php \
    php-mysql \
    php-mbstring \
    wget \
    unzip

mkdir -p /opt/download-dir
cd /opt/download-dir
wget https://files.phpmyadmin.net/phpMyAdmin/5.2.1/phpMyAdmin-5.2.1-all-languages.zip
unzip phpMyAdmin-5.2.1-all-languages.zip
mv phpMyAdmin-5.2.1-all-languages /var/www/html/phpmyadmin
rm -rf /opt/download-dir
mkdir -p /var/www/html/phpmyadmin/tmp/
chmod 777 /var/www/html/phpmyadmin/tmp/

cp phpmyadmin/config.inc.php /var/www/html/phpmyadmin/config.inc.php

systemctl restart apache2
```
