FROM php:8.1.8-apache

RUN apt-get clean all
RUN apt-get update
RUN apt-get dist-upgrade -y

RUN apt-get install -y wget zip libcurl4-openssl-dev libpq-dev libzip-dev libjpeg62-turbo-dev libpng-dev libfreetype6-dev libonig-dev libapache2-mod-xsendfile jpegoptim optipng pngquant webp npm gifsicle pkg-config imagemagick libmpdec-dev libmemcached-dev

RUN apt-get update && apt-get install -y libmagickwand-dev --no-install-recommends && rm -rf /var/lib/apt/lists/*

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN pecl install redis

RUN echo "extension=redis.so" > /usr/local/etc/php/conf.d/10_redis.ini

RUN pecl install memcached

#RUN mkdir -p /usr/src/php/ext/imagick; \
#    curl -fsSL https://github.com/Imagick/imagick/archive/06116aa24b76edaf6b1693198f79e6c295eda8a9.tar.gz | tar xvz -C "/usr/src/php/ext/imagick" --strip 1; \
#    docker-php-ext-install imagick;

RUN echo "extension=memcached.so" > /usr/local/etc/php/conf.d/20_memcached.ini

RUN pecl install decimal

RUN echo "extension=decimal.so" > /usr/local/etc/php/conf.d/30_decimal.ini

RUN pecl install imagick

RUN echo "extension=imagick.so" > /usr/local/etc/php/conf.d/40_imagick.ini

RUN pecl install mongodb

RUN echo "extension=mongodb.so" > /usr/local/etc/php/conf.d/50_mongodb.ini

RUN a2enmod proxy
RUN a2enmod proxy_http
RUN a2enmod proxy_balancer
RUN a2enmod lbmethod_byrequests
RUN a2enmod proxy_ajp
RUN a2enmod proxy_connect
RUN a2enmod proxy_html

RUN docker-php-ext-install pdo_mysql mbstring zip exif intl soap xml curl mysqli calendar

RUN docker-php-ext-configure gd \
--with-freetype=/usr/include/ \
--with-jpeg=/usr/include/

RUN docker-php-ext-install gd

RUN npm install -g svgo

RUN mkdir -p /tmp/pear/cache

RUN mkdir /app

RUN chown -R www-data:www-data /app && a2enmod rewrite && a2enmod headers

RUN apt update -y

RUN apt-get install -y gnupg

RUN curl https://packages.stripe.dev/api/security/keypair/stripe-cli-gpg/public | apt-key add -

RUN echo "deb https://packages.stripe.dev/stripe-cli-debian-local stable main" | tee -a /etc/apt/sources.list

RUN apt update -y

RUN apt install -y stripe