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

* [`cli`, `latest` (7.1/cli/Dockerfile)](https://github.com/hurtom/php/blob/master/7.1/cli/Dockerfile)
* [`fpm` (7.1/fpm/Dockerfile)](https://github.com/hurtom/php/blob/master/7.1/fpm/Dockerfile)
* [`nginx` (7.1/nginx/Dockerfile)](https://github.com/hurtom/php/blob/master/7.1/nginx/Dockerfile)
