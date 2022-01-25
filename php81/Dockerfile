FROM php:8.1-fpm

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get -y --no-install-recommends install apt-utils g++ imagemagick libc-client-dev
RUN apt-get -y --no-install-recommends install libcurl4-openssl-dev libfreetype6-dev libgd-dev libicu-dev libkrb5-dev
RUN apt-get -y --no-install-recommends install libmcrypt-dev libpng-dev libxml2-dev libsnmp-dev openssl snmp wkhtmltopdf
RUN apt-get -y --no-install-recommends install libxslt-dev zlib1g-dev libjpeg-dev libfreetype6-dev libmagickwand-dev
RUN apt-get -y --no-install-recommends install libsodium-dev libzip-dev libgmp-dev unzip libwebp-dev
RUN apt-get -y --no-install-recommends install libmagickcore-dev libyaml-dev

RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl
RUN docker-php-ext-install imap
RUN pecl install imagick
RUN docker-php-ext-install exif pdo curl dom pdo_mysql iconv intl sodium phar snmp session
RUN CFLAGS="$CFLAGS -D_GNU_SOURCE" docker-php-ext-install sockets
RUN docker-php-ext-configure gd --with-freetype --with-jpeg  --with-webp
RUN docker-php-ext-install gd
RUN docker-php-ext-install xml xsl xmlwriter zip soap bcmath mysqli
RUN docker-php-ext-configure gmp
RUN docker-php-ext-install gmp
RUN pecl install xdebug
RUN pecl install yaml
RUN docker-php-ext-enable xdebug
RUN docker-php-ext-enable imagick
RUN docker-php-ext-enable yaml

RUN apt-get clean
RUN rm -rf /tmp/* /var/tmp/* /usr/share/doc/*
