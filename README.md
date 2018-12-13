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

See an example [nginx.conf](https://github.com/hurtom/php/blob/master/7.2/debian/nginx/nginx.conf)

#### CLI

```
docker run -it --rm hurtom/php:cli php -v
```

#### Tags

* [`7.2-cli`, `cli`, `latest` (7.2/debian/cli/Dockerfile)](https://github.com/hurtom/php/blob/master/7.2/debian/cli/Dockerfile)
* [`7.2-fpm`, `fpm` (7.2/debian/fpm/Dockerfile)](https://github.com/hurtom/php/blob/master/7.2/debian/fpm/Dockerfile)
* [`7.2-nginx`, `nginx` (7.2/debian/nginx/Dockerfile)](https://github.com/hurtom/php/blob/master/7.2/debian/nginx/Dockerfile)

* [`7.2-cli-alpine`, `cli-alpine` (7.2/alpine/cli/Dockerfile)](https://github.com/hurtom/php/blob/master/7.2/alpine/cli/Dockerfile)
* [`7.2-fpm-alpine`, `fpm-alpine` (7.2/alpine/fpm/Dockerfile)](https://github.com/hurtom/php/blob/master/7.2/alpine/fpm/Dockerfile)
* [`7.2-nginx-alpine`, `nginx-alpine` (7.2/alpine/nginx/Dockerfile)](https://github.com/hurtom/php/blob/master/7.2/alpine/nginx/Dockerfile)

* [`5.6-cli` (5.6/debian/cli/Dockerfile)](https://github.com/hurtom/php/blob/master/5.6/debian/cli/Dockerfile)
* [`5.6-fpm` (5.6/debian/fpm/Dockerfile)](https://github.com/hurtom/php/blob/master/5.6/debian/fpm/Dockerfile)
* [`5.6-nginx` (5.6/debian/nginx/Dockerfile)](https://github.com/hurtom/php/blob/master/5.6/debian/nginx/Dockerfile)

* [`5.6-cli-alpine` (5.6/alpine/cli/Dockerfile)](https://github.com/hurtom/php/blob/master/5.6/alpine/cli/Dockerfile)
* [`5.6-fpm-alpine` (5.6/alpine/fpm/Dockerfile)](https://github.com/hurtom/php/blob/master/5.6/alpine/fpm/Dockerfile)
* [`5.6-nginx-alpine` (5.6/alpine/nginx/Dockerfile)](https://github.com/hurtom/php/blob/master/5.6/alpine/nginx/Dockerfile)

**Note:** `alpine` images have a slightly different behavior. Make sure to test before going into production
