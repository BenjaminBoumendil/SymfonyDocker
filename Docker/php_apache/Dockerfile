FROM ubuntu:16.10

MAINTAINER Benjamin Boumendil

RUN apt-get update

RUN apt-get install -y apache2

RUN apt-get install -y php7.0-common php7.0-cli libapache2-mod-php7.0

RUN apt-get install -y php7.0-mcrypt php7.0-mysql php7.0-apcu php7.0-curl php7.0-intl php7.0-xdebug

ADD php-custom.ini /etc/php7.0/apache2/conf.d
ADD 20-xdebug.ini /etc/php7.0/apache2/conf.d
ADD php-custom.ini /etc/php7.0/cli/conf.d
ADD 20-xdebug.ini /etc/php7.0/cli/conf.d

RUN php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/local/bin --filename=composer \
    && chmod +x /usr/local/bin/composer

RUN apt-get install -y git

EXPOSE 80

WORKDIR /etc/php7.0

CMD /usr/sbin/apache2ctl -D FOREGROUND
