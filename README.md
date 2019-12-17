# Laravel on AlterVista

We start this project using the [PHP Docker official image](https://hub.docker.com/_/php)

If exists stop any running server on port 80, for example `sudo apachectl stop` and If you need space clean all your old docker images with `docker system prune -a`

Build the current project and run it:

```
docker build -t laravista .
docker run -d --rm -p 80:80 -v "$PWD/src":/var/www/html --name running laravista
```

Open this URL http://127.0.0.1/info.php and try to modify the PHP page:

```
<?php
// phpinfo();
echo "UPDATE";
```

Check the result and if ok stop the container `docker stop running`

## Composer

Install Composer into Dockerfile:

```
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
```

build, run it and go into to check the command version:

```
docker exec -it running bash
composer --version
```

## Laravel 5.6

Install zip/unzip into Dockerfile:

```
RUN apt-get update && apt-get install -y zip unzip
```

build, run it and go into to create a new `L56` project:

```
composer create-project --prefer-dist laravel/laravel L56 "5.6.*"```
```

check the correct Laravel page http://127.0.0.1/L56/public/

Zip the folder `zip -r L56.zip L56` and upload the archive on AlterVista to see this error:

```
[2019-12-17 22:15:05] production.ERROR: No application encryption key has been specified. {"exception":"[object] (RuntimeException(code: 0): No application encryption key has been specified. at /membri/laravista/L56/vendor/laravel/framework/src/Illuminate/Encryption/EncryptionServiceProvider.php:42)
```

https://laravista.altervista.org/L56/storage/logs/laravel.log
