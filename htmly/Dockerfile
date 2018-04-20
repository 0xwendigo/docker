FROM php:5.6.35-apache-jessie
MAINTAINER Alexandre Schwartzmann <schwartzmann.a@gmail.com>

LABEL version="1.0"
LABEL os-version="debian:jessie"
LABEL apache-version="2.4"
LABEL php-version="5.6.35"

ENV ACCEPT_EULA Y

ADD installer.php /var/www/html/
ADD htmly.conf /etc/apache2/sites-available/

RUN chmod 777 /var/log/httpd/
RUN a2enmod rewrite


EXPOSE 80

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
