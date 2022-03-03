# Magento 2 Cloud Docker

Collection of Magento 2 Cloud Docker docker-compose configuration files for running open source with Magento 2 Cloud Docker development environment.

## How these are built

Using development tool from here

    https://github.com/magento/magento-cloud

    ./vendor/bin/ece-docker build:compose

## Steps

### 2.4.3

    curl -sL https://github.com/magento/magento-cloud/archive/2.4.3.tar.gz | tar xz
    mv magento-cloud-2.4.3/{.,}* ./
    rm magento-cloud-2.4.3 -rf
    wget -qO- https://magento.mirror.hypernode.com/releases/magento2-2.4.3.tar.gz | tar xfz -
    composer require magento/ece-tools symfony/config:^4.4 symfony/console:^4.0 symfony/dependency-injection:^4.3 symfony/process:^4.1 symfony/serializer:^4.0 symfony/yaml:^4.0 -v

### Example command to generate docker-compose.yml

`./vendor/bin/ece-docker build:compose --mode="developer" --php="7.3" --nginx="1.19" --expose-db-port="3306" --no-varnish`

### Command parameters

    build:compose   [--php PHP] 
                    [--nginx NGINX] 
                    [--db DB] 
                    [--db-image DB-IMAGE] 
                    [--expose-db-port EXPOSE-DB-PORT] 
                    [--expose-db-quote-port EXPOSE-DB-QUOTE-PORT] 
                    [--expose-db-sales-port EXPOSE-DB-SALES-PORT] 
                    [--with-entrypoint] 
                    [--with-mariadb-conf] 
                    [--redis REDIS]
                    [--es ES] 
                    [--rmq RMQ] 
                    [--node NODE]
                    [--selenium-version SELENIUM-VERSION]
                    [--selenium-image SELENIUM-IMAGE]
                    [--zookeeper-version ZOOKEEPER-VERSION]
                    [--zookeeper-image ZOOKEEPER-IMAGE]
                    [--no-es]
                    [--no-mailhog]
                    [--mailhog-smtp-port MAILHOG-SMTP-PORT]
                    [--mailhog-http-port MAILHOG-HTTP-PORT]
                    [--set-docker-host]
                    [--nginx-worker-processes [NGINX-WORKER-PROCESSES]]
                    [--nginx-worker-connections [NGINX-WORKER-CONNECTIONS]]
                    [--custom-registry [CUSTOM-REGISTRY]]
                    [-m|--mode MODE]
                    [--sync-engine SYNC-ENGINE]
                    [--with-cron]
                    [--no-varnish]
                    [--with-selenium]
                    [--with-zookeeper]
                    [--with-test] [--no-tmp-mounts]
                    [--with-xdebug]
                    [--env-vars [ENV-VARS]]
                    [--installation-type [INSTALLATION-TYPE]]
                    [--host HOST]
                    [--port PORT]
                    [--no-tls]
                    [--tls-port TLS-PORT]
                    [--es-env-var ES-ENV-VAR]
                    [--db-increment-increment DB-INCREMENT-INCREMENT]
                    [--db-increment-offset DB-INCREMENT-OFFSET]
                    [--root-dir ROOT-DIR]
