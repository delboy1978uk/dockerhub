FROM php:8.6-fpm-bookworm

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

RUN docker-php-ext-install exif pdo_mysql intl snmp
RUN CFLAGS="$CFLAGS -D_GNU_SOURCE" docker-php-ext-install sockets
RUN docker-php-ext-configure gd --with-freetype --with-jpeg  --with-webp
RUN docker-php-ext-configure gmp
RUN docker-php-ext-install gd xsl zip soap bcmath mysqli pcntl gmp

# PHP 8.6's image has no pecl (PEAR is gone): extensions come from PIE
# (https://github.com/php/pie), or are built from git where no release
# supports 8.6 yet. Move to stable versions as they come out.
COPY --from=ghcr.io/php/pie:bin /pie /usr/bin/pie
RUN pie install "xdebug/xdebug:^3.6@alpha"
RUN pie install "phpredis/phpredis:6.4.0RC1"
RUN pie install pecl/yaml
RUN git clone --depth 1 https://github.com/Imagick/imagick /tmp/imagick && cd /tmp/imagick && phpize && ./configure && make && make install
RUN git clone --depth 1 https://github.com/php/pecl-mail-imap /tmp/imap && cd /tmp/imap && phpize && ./configure --with-kerberos --with-imap-ssl && make && make install
RUN docker-php-ext-enable imagick imap
RUN php -m | grep -qx redis && php -m | grep -qx xdebug && php -m | grep -qx yaml && php -m | grep -qx imagick && php -m | grep -qx imap
RUN apt-get clean
RUN rm -rf /tmp/* /var/tmp/* /usr/share/doc/*
