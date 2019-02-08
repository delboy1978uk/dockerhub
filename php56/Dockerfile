FROM php:5.6.30-fpm

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
RUN apt-get -y --no-install-recommends install libjpeg-dev
RUN apt-get -y --no-install-recommends install libpng-dev
RUN apt-get -y --no-install-recommends install libxml2-dev
RUN apt-get -y --no-install-recommends install libsnmp-dev
RUN apt-get -y --no-install-recommends install openssl
RUN apt-get -y --no-install-recommends install php5-imagick
RUN apt-get -y --no-install-recommends install php5-xdebug
RUN apt-get -y --no-install-recommends install snmp
RUN apt-get update
RUN apt-get -y --no-install-recommends install ssmtp
RUN apt-get -y --no-install-recommends install wkhtmltopdf
RUN apt-get -y --no-install-recommends install libxslt-dev
RUN apt-get -y --no-install-recommends install zlib1g-dev
RUN apt-get -y --no-install-recommends install libjpeg-dev
RUN apt-get -y --no-install-recommends install libfreetype6-dev

RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl
RUN docker-php-ext-install imap
RUN docker-php-ext-configure gd --with-freetype-dir=/usr --with-jpeg-dir=/usr
RUN docker-php-ext-install gd exif pdo curl dom pdo_mysql iconv intl mcrypt hash phar session snmp sockets xml xmlreader xmlrpc xmlwriter xsl zip

RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php --filename=composer
RUN php -r "unlink('composer-setup.php');"
RUN mv ./composer /usr/bin/composer

RUN apt-get -y --no-install-recommends install git
RUN apt-get -y --no-install-recommends install zsh
RUN apt-get -y --no-install-recommends install wget
ENV TERM xterm
RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true

RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*
RUN echo 'export PATH=$PATH:vendor/bin' > ~/.zshrc
