# Magento 2 Cloud Docker

Collection of Magento 2 Cloud Docker docker-compose configuration files

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
    ./vendor/bin/ece-docker build:compose --mode="default" --php="7.3" --nginx="1.19" --expose-db-port="3306" --no-varnish
