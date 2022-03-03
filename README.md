# WIP Modular Cloud Docker Compose

Collection of Magento 2 Cloud Docker docker-compose configuration files for running open source with Magento 2 Cloud Docker development environment.

## 1 Fetch from git

git clone git@github.com:DominicWatts/Magento2CloudDocker.git ./

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

docker-compose -f php74.yml up -d