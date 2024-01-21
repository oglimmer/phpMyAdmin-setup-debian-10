FROM debian:10

RUN apt-get update && apt-get install -y \
    apache2 \
    php \
    php-mysql \
    php-mbstring \
    wget \
    unzip

RUN mkdir -p /opt/download-dir && cd /opt/download-dir && \
    wget https://files.phpmyadmin.net/phpMyAdmin/5.2.1/phpMyAdmin-5.2.1-all-languages.zip && \
    unzip phpMyAdmin-5.2.1-all-languages.zip && \
    mv phpMyAdmin-5.2.1-all-languages /var/www/html/phpmyadmin && \
    rm -rf /opt/download-dir && \
    mkdir -p /var/www/html/phpmyadmin/tmp/ && \
    chmod 777 /var/www/html/phpmyadmin/tmp/

COPY config.inc.php /var/www/html/phpmyadmin/config.inc.php

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
