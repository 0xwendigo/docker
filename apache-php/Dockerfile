FROM alpine:3.5
MAINTAINER Alexandre Schwartzmann <schwartzmann.a@gmail.com>

LABEL version="1.0"
LABEL os-version="alpine:3.5"
LABEL apache-version="2.4"
LABEL php-version="7.0"

ENV ACCEPT_EULA Y

RUN apk add --no-cache apache2 apache2-ssl php7 php7-apache2 php7-mysqlnd php7-mysqli php7-gd php7-gettext php7-pgsql

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

ADD .htaccess /var/www/localhost/htdocs/
ADD .htpasswd /var/www/localhost/htdocs/
ADD phpinfo.php /var/www/localhost/htdocs/
ADD testsql.php /var/www/localhost/htdocs/

RUN ln -sf ./phpinfo.php /var/www/localhost/htdocs/index.php
RUN mv /var/www/localhost/htdocs/index.html /var/www/localhost/htdocs/index.html.orig

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
