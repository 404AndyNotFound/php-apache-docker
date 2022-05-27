# PHP Apache Docker
A Docker setup running PHP 7.4 and 8.1 side by side.

## What is included?

Includes:

- Nginx reverse proxy
- PHP 7.4
- PHP 8.1
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