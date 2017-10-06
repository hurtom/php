#### docker-compose Nginx

```
  server:
    image: hurtom/php:nginx
    restart: always
    ports:
      - "8080:80"
    volumes:
      - ./:/var/www/html
      - ./php.ini:/usr/local/etc/php/php.ini
```

#### docker-compose FPM

```
  server:
    image: nginx:mainline
    restart: always
    ports:
      - "8080:80"
    volumes:
      - ./:/var/www/html
      - ./nginx.conf:/etc/nginx/nginx.conf

  fpm:
    image: hurtom/php:fpm
    restart: always
    volumes:
      - ./:/var/www/html
      - ./php.ini:/usr/local/etc/php/php.ini
```

See an example [nginx.conf](https://github.com/hurtom/php/blob/master/7.1/nginx/nginx.conf)

#### CLI

```
docker run -it --rm hurtom/php:cli php -v
```

#### Tags

* [`7.1-cli`, `cli`, `latest` (7.1/cli/Dockerfile)](https://github.com/hurtom/php/blob/master/7.1/cli/Dockerfile)
* [`7.1-fpm`, `fpm` (7.1/fpm/Dockerfile)](https://github.com/hurtom/php/blob/master/7.1/fpm/Dockerfile)
* [`7.1-nginx`, `nginx` (7.1/nginx/Dockerfile)](https://github.com/hurtom/php/blob/master/7.1/nginx/Dockerfile)

* [`7.1-cli-alpine`, `alpine` (7.1/alpine/cli/Dockerfile)](https://github.com/hurtom/php/blob/master/7.1/alpine/cli/Dockerfile)
* [`7.1-fpm-alpine`, `fpm-alpine` (7.1/alpine/fpm/Dockerfile)](https://github.com/hurtom/php/blob/master/7.1/alpine/fpm/Dockerfile)
* [`7.1-nginx-alpine`, `nginx-alpine` (7.1/alpine/nginx/Dockerfile)](https://github.com/hurtom/php/blob/master/7.1/alpine/nginx/Dockerfile)

* [`5.6-cli` (5.6/cli/Dockerfile)](https://github.com/hurtom/php/blob/master/5.6/cli/Dockerfile)
* [`5.6-fpm` (5.6/fpm/Dockerfile)](https://github.com/hurtom/php/blob/master/5.6/fpm/Dockerfile)
* [`5.6-nginx` (5.6/nginx/Dockerfile)](https://github.com/hurtom/php/blob/master/5.6/nginx/Dockerfile)
