# PHP Apache Docker
A Docker setup running PHP 7.4 and 8.1 side by side.

## What is included?

Included Containers:

- NGINX (reverse proxy)
- PHP 7.4 + Apache
- PHP 8.1 + Apache
- [Redis](https://redis.io/)
- [Memcached](https://memcached.org/)
- [MariaDB](https://mariadb.com/)


Both PHP containers are configured with:

- [Composer](https://getcomposer.org/)
- [Decimal](https://php-decimal.io/)
- [ImageMagick](https://imagemagick.org/)
- [Imagick](https://www.php.net/manual/en/class.imagick.php)
- [Memcached](https://www.php.net/manual/en/book.memcached.php)
- [XSendFile](https://tn123.org/mod_xsendfile/)
- [PhpRedis](https://github.com/phpredis/phpredis)

## Installation

```
docker-compose up --build -d
```

## Configuration / Usage

Configure a site in the reverse proxy in ```nginx.conf```

Configure for PHP 8.1
```
server { # simple reverse-proxy
    listen 80;
    server_name <<Your site's domain>>;

    location / {
      include /etc/nginx/includes/proxy.conf;
      proxy_pass http://php81;
    }
} 
```

Configure for PHP 7.4
```
server { # simple reverse-proxy
    listen 80;
    server_name <<Your site's domain>>;

    location / {
      include /etc/nginx/includes/proxy.conf;
      proxy_pass http://php74;
    }
} 
```