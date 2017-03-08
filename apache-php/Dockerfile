FROM ubuntu:xenial
MAINTAINER Alexandre Schwartzmann <schwartzmann.a@gmail.com>

LABEL version="1.0"
LABEL os-version="ubuntu:xenial"
LABEL apache-version="2.4"
LABEL php-version="7.0"

ENV ACCEPT_EULA Y

RUN apt-get update && apt-get -y install apt-transport-https
RUN sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/mssql-ubuntu-xenial-release/ xenial main" > /etc/apt/sources.list.d/mssqlpreview.list'
RUN apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
RUN apt-get update && apt-get -y install apache2 php7.0 libapache2-mod-php php-mysql php-mysqlnd php-mysqli php-sybase php-gd php-gettext php7.0-pgsql msodbcsql unixodbc-dev-utf16 && apt-get clean && rm -rf /var/lib/apt/lists/*

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

RUN /usr/sbin/a2ensite default-ssl
RUN /usr/sbin/a2enmod ssl
RUN /usr/sbin/a2dismod 'mpm_*' && /usr/sbin/a2enmod mpm_prefork
RUN /usr/sbin/a2enmod php7.0

RUN pecl install sqlsrv
RUN pecl install pdo_sqlsrv
RUN echo "extension=/usr/lib/php/20151012/sqlsrv.so" >> /etc/php/7.0/apache2/php.ini
RUN echo "extension=/usr/lib/php/20151012/pdo_sqlsrv.so" >> /etc/php/7.0/apache2/php.ini
RUN echo "extension=/usr/lib/php/20151012/sqlsrv.so" >> /etc/php/7.0/cli/php.ini
RUN echo "extension=/usr/lib/php/20151012/pdo_sqlsrv.so" >> /etc/php/7.0/cli/php.ini

ADD .htaccess /var/www/html/
ADD .htpasswd /var/www/html/
ADD phpinfo.php /var/www/html/
ADD testsql.php /var/www/html/

RUN ln -sf ./phpinfo.php /var/www/html/index.php
RUN mv /var/www/html/index.html /var/www/html/index.html.orig

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
