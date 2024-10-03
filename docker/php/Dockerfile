FROM php:8.2-fpm

RUN apt-get update && apt-get upgrade -y \
    && apt-get install git zip vim libzip-dev libgmp-dev libffi-dev libssl-dev libpng-dev libcurl4-openssl-dev libicu-dev libpq-dev wget jq curl -y \
    && docker-php-ext-install -j$(nproc) gd sockets zip curl intl gmp pcntl bcmath ffi pdo pdo_mysql pdo_pgsql \
    && docker-php-source delete \
    && apt-get autoremove --purge -y && apt-get autoclean -y && apt-get clean -y

RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
    && apt-get install -y nodejs \
    && npm install -g npm@latest

COPY ./docker/php/install-composer.sh /
RUN sh /install-composer.sh

COPY ./docker/php/php.ini /usr/local/etc/php/

RUN chown -R www-data:www-data /var/www/html
WORKDIR /var/www/html

RUN chmod -R 777 /var/www/html

#EXPOSE 9000
CMD [ "docker-php-entrypoint", "php-fpm" ]
