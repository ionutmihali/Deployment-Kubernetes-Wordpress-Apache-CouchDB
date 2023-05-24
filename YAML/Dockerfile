FROM php:8.0-apache

RUN apt-get update && apt-get install -y \
    libcurl4-openssl-dev \
    pkg-config \
    libssl-dev \
    lsb-release \
    wget \
    zlib1g-dev \
    cmake

RUN docker-php-ext-install pdo pdo_mysql

# Install Couchbase PHP extension
RUN pecl install couchbase \
    && docker-php-ext-enable couchbase

EXPOSE 80 443

COPY index.php /var/www/html

CMD apachectl -D FOREGROUND