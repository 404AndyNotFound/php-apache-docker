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

### Reverse Proxy

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

After editing ```nginx.conf``` make sure to restart the nginx container ```docker restart nginx```

### Virtual Hosts

#### PHP 8.1

Place your web files in a subdirectory inside the ```www``` folder

Edit ```vhost8.1.conf```

```
<VirtualHost *:80>
    ServerName <<Your site's domain>>
    DocumentRoot /var/www/html/<<<Your site's folder name>>>/public_html
    <Directory /var/www/html/<<<Your site's folder name>>>/public_html>
           
        AllowOverride All
        Require all granted

    XSendFile On
        XSendFilePath /var/www/html/<<<Your site's folder name>>>
    </Directory>
</VirtualHost>
```

After editing ```vhost8.1.conf``` make sure to restart the nginx container ```docker restart php81```

#### PHP 7.4

Place your web files in a subdirectory inside the ```www``` folder

Edit ```vhost7.4.conf```

```
<VirtualHost *:80>
    ServerName <<Your site's domain>>
    DocumentRoot /var/www/html/<<<Your site's folder name>>>/public_html
    <Directory /var/www/html/<<<Your site's folder name>>>/public_html>
           
        AllowOverride All
        Require all granted

    XSendFile On
        XSendFilePath /var/www/html/<<<Your site's folder name>>>
    </Directory>
</VirtualHost>
```

After editing ```vhost7.4.conf``` make sure to restart the nginx container ```docker restart php74```

## Hosts

Edit your host file and add a line similar to the following:

```
127.0.0.1   <<<Your site's domain>>>
```