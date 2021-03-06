# Magento 2 Open Docker

Boilerplate for docker-compose inside projects using official magento images. Can be used to run Open Source edition.

Uses the following images

## master branch

[magento/magento-cloud-docker-php](https://hub.docker.com/r/magento/magento-cloud-docker-php)

[magento/magento-cloud-docker-nginx](https://hub.docker.com/r/magento/magento-cloud-docker-nginx)

[magento/magento-cloud-docker-varnish](https://hub.docker.com/r/magento/magento-cloud-docker-varnish)

[magento/magento-cloud-docker-elasticsearch](https://hub.docker.com/r/magento/magento-cloud-docker-elasticsearch)

## unofficial-images branch

[domw/magento2-cloud-php](https://hub.docker.com/r/domw/magento2-cloud-php)

[domw/magento2-cloud-nginx](https://hub.docker.com/r/domw/magento2-cloud-nginx)

[domw/magento2-cloud-varnish](https://hub.docker.com/r/domw/magento2-cloud-varnish)

[domw/magento2-cloud-elasticsearch](https://hub.docker.com/r/domw/magento2-cloud-elasticsearch)

[domw/magento2-cloud-tls](https://hub.docker.com/r/domw/magento2-cloud-elasticsearch)

Plus official non-Magento images for the remaining containers.

Image builds are found here:

### Official

[Github](https://github.com/magento/magento-cloud-docker)

[Images](https://github.com/magento/magento-cloud-docker/tree/develop/images)

### Unofficial

[Github](https://github.com/DominicWatts/Magento2CloudDocker)

[Images](https://github.com/DominicWatts/Magento2CloudDocker/tree/master/images)

## Start with Quickstart

[Quickstart Guide](QUICKSTART.md)

## Usage

### Helper script

    ./bin/local
    
### Getting started

Extract Magento open source to `./`

### Generic

Pull

    docker-compose pull

Up / Down / Start / Stop

    docker-compose up -d
    docker-compose down -v
    docker-compose start
    docker-compose stop
    
Restart

    docker-compose restart
    
### Bash

    docker-compose run --rm cli
    
Or

    docker-compose run --rm cli bash 

Or specific config

    docker-compose -f docker-compose.no.varnish.yml up -d

    docker-compose -f docker-compose.no.varnish.yml run --rm cli
    
### Magento command

    docker-compose run --rm cli magento-command

### Run cron

#### Container binary 

    docker-compose run --rm cli run-cron

#### Or safer - command within container

    docker-compose run --rm cli magento-command cron:run
    
#### Or even safer - configure cron container

```yml
  cron:
    hostname: cron.magento2.docker
    image: 'magento/magento-cloud-docker-php:7.3-cli-1.2.0'
    extends: generic
    command: run-cron
    environment:
      CRONTAB: '* * * * * root cd /app && /usr/local/bin/php bin/magento cron:run >> /app/var/log/cron.log'
    volumes:
      - '.:/app'
    networks:
      magento:
        aliases:
          - cron.magento2.docker   
```

### Run CLI installer

With files extracted to `/.` run CLI install process

    docker-compose run --rm cli magento-command setup:install --admin-firstname Admin --admin-lastname User [...]

### Flush redis

    docker-compose exec redis redis-cli FLUSHALL
    
### Flush varnish

    docker-compose exec varnish varnishadm ban req.url '~' '.'
    
### Access DB CLI

    docker-compose exec db sh -c 'mysql -u magento2 -pmagento2 magento2 "$@"'

### Tweaks

PHP settings can be adjusted via

    ./php.ini

## Mailhog

### Container

```yml
  mail:
    image: mailhog/mailhog:latest
    restart: 'always'
    ports:
      - 1025:1025
      - 8025:8025
    links:
      - fpm
      - db
    networks:
      - magento
```

### SMTP extension config

  -  host: `mail`
  -  port: `1025`
  -  protocol: `none`
  -  authentication: `plain`


### Run Mode

```yml
generic:
    hostname: generic.magento2.docker
    image: 'magento/magento-cloud-docker-php:7.3-cli-1.2.0'
    environment:
      - MAGENTO_RUN_MODE=default
      - 'PHP_EXTENSIONS=bcmath bz2 calendar exif gd gettext intl mysqli pcntl pdo_mysql soap sockets sysvmsg sysvsem sysvshm opcache zip redis xsl ioncube'
```

### Elasticsearch

How to disable ElasticSearch disk quota / watermark

Find elasticsearch container

    docker exec -it ffbcd5a4e1b8 bash

    curl -XPUT -H "Content-Type: application/json" http://localhost:9200/_all/_settings -d '{"index.blocks.read_only_allow_delete": null}'
