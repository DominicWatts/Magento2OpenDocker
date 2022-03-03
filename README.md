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


## Edit host file

127.0.0.1 magento2.docker
## Using docker

### Download Magento to work directory

    wget -qO- https://magento.mirror.hypernode.com/releases/magento2-2.4.3.tar.gz | tar xfz -
    
### Add docker config

    touch docker-composer.yml

    [edit docker.compose.yml]
    
### Create environment file

```
mkdir .docker
touch .docker/config.env
```

#### Example config.env

    MAGENTO_CLOUD_RELATIONSHIPS=eyJkYXRhYmFzZSI6W3siaG9zdCI6ImRiIiwicGF0aCI6Im1hZ2VudG8yIiwicGFzc3dvcmQiOiJtYWdlbnRvMiIsInVzZXJuYW1lIjoibWFnZW50bzIiLCJwb3J0IjoiMzMwNiIsInR5cGUiOiJteXNxbDoxMC4zIn1dLCJyZWRpcyI6W3siaG9zdCI6InJlZGlzIiwicG9ydCI6IjYzNzkiLCJ0eXBlIjoicmVkaXM6NS4wIn1dLCJlbGFzdGljc2VhcmNoIjpbeyJob3N0IjoiZWxhc3RpY3NlYXJjaCIsInBvcnQiOiI5MjAwIiwidHlwZSI6ImVsYXN0aWNzZWFyY2g6Ny43In1dfQ==
    MAGENTO_CLOUD_ROUTES=eyJodHRwOlwvXC9tYWdlbnRvMi5kb2NrZXJcLyI6eyJ0eXBlIjoidXBzdHJlYW0iLCJvcmlnaW5hbF91cmwiOiJodHRwOlwvXC97ZGVmYXVsdH0ifSwiaHR0cHM6XC9cL21hZ2VudG8yLmRvY2tlclwvIjp7InR5cGUiOiJ1cHN0cmVhbSIsIm9yaWdpbmFsX3VybCI6Imh0dHBzOlwvXC97ZGVmYXVsdH0ifX0=
    MAGENTO_CLOUD_VARIABLES=eyJBRE1JTl9FTUFJTCI6ImFkbWluQGV4YW1wbGUuY29tIiwiQURNSU5fUEFTU1dPUkQiOiIxMjMxMjNxIiwiQURNSU5fVVJMIjoiYWRtaW4ifQ==
    MAGENTO_CLOUD_APPLICATION=eyJob29rcyI6eyJidWlsZCI6InNldCAtZVxucGhwIC5cL3ZlbmRvclwvYmluXC9lY2UtdG9vbHMgcnVuIHNjZW5hcmlvXC9idWlsZFwvZ2VuZXJhdGUueG1sXG5waHAgLlwvdmVuZG9yXC9iaW5cL2VjZS10b29scyBydW4gc2NlbmFyaW9cL2J1aWxkXC90cmFuc2Zlci54bWxcbiIsImRlcGxveSI6InBocCAuXC92ZW5kb3JcL2JpblwvZWNlLXRvb2xzIHJ1biBzY2VuYXJpb1wvZGVwbG95LnhtbFxuIiwicG9zdF9kZXBsb3kiOiJwaHAgLlwvdmVuZG9yXC9iaW5cL2VjZS10b29scyBydW4gc2NlbmFyaW9cL3Bvc3QtZGVwbG95LnhtbFxuIn0sIm1vdW50cyI6eyJ2YXIiOnsicGF0aCI6InZhciIsIm9yaWciOiJzaGFyZWQ6ZmlsZXNcL3ZhciJ9LCJhcHBcL2V0YyI6eyJwYXRoIjoiYXBwXC9ldGMiLCJvcmlnIjoic2hhcmVkOmZpbGVzXC9ldGMifSwicHViXC9tZWRpYSI6eyJwYXRoIjoicHViXC9tZWRpYSIsIm9yaWciOiJzaGFyZWQ6ZmlsZXNcL21lZGlhIn0sInB1Ylwvc3RhdGljIjp7InBhdGgiOiJwdWJcL3N0YXRpYyIsIm9yaWciOiJzaGFyZWQ6ZmlsZXNcL3N0YXRpYyJ9fX0=
    PHP_MEMORY_LIMIT=2048M
    UPLOAD_MAX_FILESIZE=64M
    MAGENTO_ROOT=/app
    PHP_IDE_CONFIG=serverName=magento_cloud_docker
    XDEBUG_CONFIG=remote_host=host.docker.internal
    INSTALLATION_TYPE=composer

### Bring up docker

    docker-compose up -d

### Go inside shell container

    docker-compose run --rm deploy

#### Install

    bin/magento setup:install --admin-firstname Admin --admin-lastname User --admin-email dominic@xigen.co.uk --admin-user admin --admin-password test123 --base-url http://magento2.docker/ --base-url-secure https://magento2.docker/ --backend-frontname xpanel --db-host db --db-name magento2 --db-user magento2 --db-password magento2 --language en_GB --currency GBP --timezone UTC --use-rewrites 1 --session-save files --use-secure 1 --use-secure-admin 1 --elasticsearch-host elasticsearch --elasticsearch-port 9200

#### Disable 2FA

    bin/magento module:disable "Magento_TwoFactorAuth"

#### Outside shell container

#### Frontend

    https://magento2.docker/

#### Backend

    https://magento2.docker/xpanel

    admin / test123