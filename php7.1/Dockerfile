FROM php:7.1.0-fpm

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
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

RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl
RUN docker-php-ext-install imap
RUN pecl install imagick
RUN docker-php-ext-install exif
RUN docker-php-ext-install pdo
RUN docker-php-ext-install curl
RUN docker-php-ext-install dom
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install iconv
RUN docker-php-ext-install intl
RUN docker-php-ext-install mcrypt
RUN docker-php-ext-install hash
RUN docker-php-ext-install phar
RUN docker-php-ext-install session
RUN docker-php-ext-install snmp
RUN docker-php-ext-install sockets
RUN docker-php-ext-configure gd --with-freetype-dir=/usr
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include --with-jpeg-dir=/usr/include
RUN docker-php-ext-install gd
RUN docker-php-ext-install xml
RUN docker-php-ext-install xmlrpc xmlwriter xsl zip
RUN docker-php-ext-install soap

RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

RUN docker-php-ext-install bcmath

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php --filename=composer
RUN php -r "unlink('composer-setup.php');"
RUN mv ./composer /usr/bin/composer

RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

COPY ./php.ini /usr/local/etc/php/php.ini
