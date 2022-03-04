# Magento 2 Cloud Docker Compose config files

Collection of Magento 2 Cloud Docker docker-compose configuration files for running open source with Magento 2 Cloud Docker development environment.

## 1 Fetch from git

git clone git@github.com:DominicWatts/Magento2CloudDocker.git ./

rm .git -rf

## 2 Add the following entry to OS hosts file

    127.0.0.1 magento2.docker

## 3 Download

Inside `./`

### 3.1 Hypernode

    wget -qO- https://magento.mirror.hypernode.com/releases/magento2-latest.tar.gz | tar xfz -

Or

    wget -qO- https://magento.mirror.hypernode.com/releases/magento-2.3.4.tar.gz | tar xfz -

### 3.2 Direct Download
 
Download magento from https://magento.com/tech-resources/download

## 4 Start Containers

Inside `./`

docker-compose up -d

## 5 Go inside shell container

    docker-compose run --rm deploy

### 5.1 Install

    bin/magento setup:install --admin-firstname Admin --admin-lastname User --admin-email dominic@xigen.co.uk --admin-user admin --admin-password test123 --base-url http://magento2.docker/ --base-url-secure https://magento2.docker/ --backend-frontname xpanel --db-host db --db-name magento2 --db-user magento2 --db-password magento2 --language en_GB --currency GBP --timezone UTC --use-rewrites 1 --session-save files --use-secure 1 --use-secure-admin 1 --elasticsearch-host elasticsearch --elasticsearch-port 9200

### 5.2 Disable 2FA

    bin/magento module:disable "Magento_TwoFactorAuth"

## 6 Outside shell container

#### Frontend

    https://magento2.docker/

#### Backend

    https://magento2.docker/xpanel

    admin / test123
