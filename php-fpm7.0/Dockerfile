FROM php:7.0-fpm
MAINTAINER João Silva

RUN apt-get update && apt-get install -y \
    vim \
    git \ 
    unzip \
    iputils-ping \
    procps

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

#install composer plugin for parallel installs
RUN composer global require hirak/prestissimo

RUN apt-get install -y libxml2-dev \
    && docker-php-ext-install xml

RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    && docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd
    
RUN apt-get install -y \
        libzip-dev \
        zip \
  && docker-php-ext-install zip


RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install dom

CMD ["php-fpm"]

EXPOSE 9000
