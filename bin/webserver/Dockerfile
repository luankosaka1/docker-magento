FROM php:7.3-apache

# https://github.com/webgriffe/docker-php-apache-base/blob/master/Dockerfile

RUN apt-get update -y

RUN apt-get install -y \
    default-libmysqlclient-dev \
    libbz2-dev \
    libmemcached-dev \
    libsasl2-dev \
    curl \
    git \
    libfreetype6-dev \
    libicu-dev \
    libjpeg-dev \
    libldap2-dev \
    libmemcachedutil2 \
    libpng-dev \
    libpq-dev \
    libxml2-dev \
    libzip-dev

# Install xsl
RUN apt-get update \
    && apt-get install -y libxslt-dev \
    && docker-php-ext-install xsl

# Install GD
RUN apt-get update \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd

# Install Intl
RUN apt-get update \
    && apt-get install -y libicu-dev \
    && docker-php-ext-install intl

# Install Mysql
RUN docker-php-ext-install mysqli pdo_mysql

# Install soap
RUN apt-get update \
    && apt-get install -y libxml2-dev \
    && docker-php-ext-install soap

# Install Bcmath
RUN docker-php-ext-install bcmath

# Install PHP zip extension
RUN docker-php-ext-install zip

# Install xdebug
RUN pecl install xdebug && docker-php-ext-enable xdebug

# INSTALL COMPOSER
RUN export COMPOSER_ALLOW_SUPERUSER=1
RUN curl -sS https://getcomposer.org/installer | php -- \
    --install-dir=/usr/bin \
    --filename=composer

# Configure Apache Document Root
ENV APACHE_DOC_ROOT /var/www/html

# Enable Apache mod_rewrite
RUN a2enmod rewrite
