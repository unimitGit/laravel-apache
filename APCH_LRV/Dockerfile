FROM php:8.0-apache

RUN apt-get update \
    && apt install -y git nano lynx \
    && docker-php-ext-install pdo_mysql

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

#COPY 90-xdebug.ini "${PHP_INI_DIR}/conf.d"

ENV APACHE_DOCUMENT_ROOT /var/www/html/joruevo/public

RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf

RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

COPY apache2.conf /etc/apache2/

RUN a2enmod rewrite

RUN service apache2 restart
