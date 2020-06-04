FROM php:7.4-fpm

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get -y --no-install-recommends install apt-utils
RUN apt-get -y --no-install-recommends install g++
RUN apt-get -y --no-install-recommends install imagemagick
RUN apt-get -y --no-install-recommends install libc-client-dev
RUN apt-get -y --no-install-recommends install libcurl4-openssl-dev
RUN apt-get -y --no-install-recommends install libfreetype6-dev
RUN apt-get -y --no-install-recommends install libgd-dev
RUN apt-get -y --no-install-recommends install libicu-dev
RUN apt-get -y --no-install-recommends install libkrb5-dev
RUN apt-get -y --no-install-recommends install libmcrypt-dev
RUN apt-get -y --no-install-recommends install libpng-dev
RUN apt-get -y --no-install-recommends install libxml2-dev
RUN apt-get -y --no-install-recommends install libsnmp-dev
RUN apt-get -y --no-install-recommends install openssl
RUN apt-get -y --no-install-recommends install snmp
RUN apt-get -y --no-install-recommends install wkhtmltopdf
RUN apt-get -y --no-install-recommends install libxslt-dev
RUN apt-get -y --no-install-recommends install zlib1g-dev
RUN apt-get -y --no-install-recommends install libjpeg-dev
RUN apt-get -y --no-install-recommends install libfreetype6-dev
RUN apt-get -y --no-install-recommends install libmagickwand-dev
RUN apt-get -y --no-install-recommends install libmagickcore-dev
RUN apt-get -y --no-install-recommends install libsodium-dev
RUN apt-get -y --no-install-recommends install libzip-dev
RUN apt-get -y --no-install-recommends install libgmp-dev
RUN apt-get -y --no-install-recommends install unzip
RUN apt-get -y --no-install-recommends install libwebp-dev

RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl
RUN docker-php-ext-install imap
RUN pecl install imagick
RUN docker-php-ext-install exif pdo curl dom pdo_mysql iconv intl sodium phar snmp sockets session
RUN docker-php-ext-configure gd --with-freetype --with-jpeg  --with-webp
RUN docker-php-ext-install gd
RUN docker-php-ext-install xml xmlrpc xsl xmlwriter zip  xmlrpc soap bcmath
RUN docker-php-ext-configure gmp
RUN docker-php-ext-install gmp
RUN pecl -d preferred_state=beta install xdebug
RUN docker-php-ext-enable xdebug

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php --filename=composer
RUN rm composer-setup.php
RUN mv ./composer /usr/bin/composer

RUN apt-get clean
RUN rm -rf /tmp/*
RUN rm -rf /var/tmp/*
RUN rm -rf /usr/share/doc/*

#COPY ./php.ini /usr/local/etc/php/php.ini
