FROM debian:jessie
MAINTAINER Alexandre Schwartzmann <schwartzmann.a@gmail.com>

RUN apt-get update && apt-get -y install apache2 php5 libapache2-mod-php5 php5-mysqlnd php5-gd php-gettext php5-pgsql php5-sybase php5-mssql && apt-get clean && rm -rf /var/lib/apt/lists/*

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

RUN /usr/sbin/a2ensite default-ssl
RUN /usr/sbin/a2enmod ssl
RUN /usr/sbin/a2dismod 'mpm_*' && /usr/sbin/a2enmod mpm_prefork
RUN /usr/sbin/a2enmod php7.0

ADD .htaccess /var/www/html/
ADD .htpasswd /var/www/html/
ADD phpinfo.php /var/www/html/
ADD testsql.php /var/www/html/

RUN ln -sf ./phpinfo.php /var/www/html/index.php
RUN mv /var/www/html/index.html /var/www/html/index.html.orig

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
