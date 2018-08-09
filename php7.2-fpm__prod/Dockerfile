FROM php:7-fpm

# Install modules
RUN apt-get update
RUN apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libmemcached-dev \
    default-libmysqlclient-dev \
    libicu-dev \
    libpq-dev \
    zlib1g-dev \
    curl

RUN docker-php-ext-install -j$(nproc) iconv 
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install -j$(nproc) gd
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install pdo_pgsql
RUN docker-php-ext-install intl

RUN pecl install memcached-3.0.4 \
    && docker-php-ext-enable memcached

RUN echo "Europe/Moscow" > /etc/timezone; dpkg-reconfigure -f noninteractive tzdata

RUN echo "cgi.fix_pathinfo=0" >> /usr/local/etc/php/conf.d/custom.ini

CMD ["php-fpm"]