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

#### CLI

```
docker run -it --rm hurtom/php:cli php -v
```
