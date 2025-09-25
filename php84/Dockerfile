FROM php:8.4-fpm-bookworm

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get -y --no-install-recommends install apt-utils g++ imagemagick libc-client-dev
RUN apt-get -y --no-install-recommends install libcurl4-openssl-dev libfreetype6-dev libgd-dev libicu-dev libkrb5-dev
RUN apt-get -y --no-install-recommends install libmcrypt-dev libpng-dev libxml2-dev libsnmp-dev openssl snmp wkhtmltopdf
RUN apt-get -y --no-install-recommends install libxslt-dev zlib1g-dev libjpeg-dev libfreetype6-dev libmagickwand-dev
RUN apt-get -y --no-install-recommends install libsodium-dev libzip-dev libgmp-dev unzip libwebp-dev
RUN apt-get -y --no-install-recommends install libmagickcore-dev libyaml-dev
RUN apt-get -y --no-install-recommends install git ca-certificates

RUN git clone https://github.com/Imagick/imagick && cd imagick && phpize && ./configure && make && make install
RUN docker-php-ext-install exif pdo curl dom pdo_mysql iconv intl sodium snmp session
RUN CFLAGS="$CFLAGS -D_GNU_SOURCE" docker-php-ext-install sockets
RUN docker-php-ext-configure gd --with-freetype --with-jpeg  --with-webp
RUN docker-php-ext-configure gmp
RUN docker-php-ext-install gd xml xsl xmlwriter zip soap bcmath mysqli pcntl posix gmp
RUN pecl install imap
RUN pecl install xdebug
RUN pecl install yaml
RUN docker-php-ext-enable xdebug imagick yaml imap
RUN #docker-php-ext-install phar
RUN apt-get clean
RUN rm -rf /tmp/* /var/tmp/* /usr/share/doc/*
