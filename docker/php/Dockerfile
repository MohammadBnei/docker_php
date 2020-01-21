FROM php:7.3.10-fpm

RUN apt-get update && apt-get install -y libicu-dev

RUN apt-get install -y libpq-dev libxslt-dev \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pdo pdo_pgsql pgsql

RUN apt-get clean

RUN pecl install apcu
RUN docker-php-ext-enable apcu
RUN docker-php-ext-install intl opcache
RUN docker-php-ext-install xsl

WORKDIR /usr/share/nginx/html

RUN chmod -R 777 ../html

# Symfony 
# RUN apt-get install wget -y && wget https://get.symfony.com/cli/installer -O - | bash
# RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony

RUN apt-get install zip -y
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
#CMD bash -c "composer install && php-fpm"

RUN apt-get install gnupg -y
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update
RUN apt-get install yarn -y