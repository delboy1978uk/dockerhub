FROM php:7.4-fpm

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get -y --no-install-recommends install apt-utils g++ imagemagick libc-client-dev
RUN apt-get -y --no-install-recommends install libcurl4-openssl-dev libfreetype6-dev libgd-dev libicu-dev libkrb5-dev
RUN apt-get -y --no-install-recommends install libmcrypt-dev libpng-dev libxml2-dev libsnmp-dev openssl snmp wkhtmltopdf
RUN apt-get -y --no-install-recommends install libxslt-dev zlib1g-dev libjpeg-dev libfreetype6-dev libmagickwand-dev
RUN apt-get -y --no-install-recommends install libmagickcore-dev libsodium-dev libzip-dev libgmp-dev unzip libwebp-dev

RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl
RUN docker-php-ext-install imap
RUN pecl install imagick
RUN docker-php-ext-install exif pdo curl dom pdo_mysql iconv intl sodium phar snmp sockets session
RUN docker-php-ext-configure gd --with-freetype --with-jpeg  --with-webp
RUN docker-php-ext-install gd
RUN docker-php-ext-install xml xmlrpc xsl xmlwriter zip  xmlrpc soap bcmath mysqli
RUN docker-php-ext-configure gmp
RUN docker-php-ext-install gmp
RUN pecl -d preferred_state=beta install xdebug
RUN docker-php-ext-enable xdebug

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php --filename=composer
RUN rm composer-setup.php
RUN mv ./composer /usr/bin/composer
RUN chown -R 1000:staff /.composer

RUN apt-get clean
RUN rm -rf /tmp/* /var/tmp/* /usr/share/doc/*
