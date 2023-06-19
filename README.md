# Magento 2 Cloud Docker for Open Source

Collection of Magento 2 Cloud Docker docker-compose configuration files for running open source with Magento 2 Cloud Docker development environment.

## 1 Fetch from git

    git clone git@github.com:DominicWatts/Magento2OpenDocker.git ./

    rm .git -rf

## 2 Add the following entry to OS hosts file

    127.0.0.1 magento2.docker

## 3 Download

Inside `./`

### 3.1 Hypernode

    wget -qO- https://magento.mirror.hypernode.com/releases/magento2-latest.tar.gz | tar xfz -

Or

    wget -qO- https://magento.mirror.hypernode.com/releases/magento-2.3.4.tar.gz | tar xfz -
    
Or

    composer create-project --repository-url=https://mirror.mage-os.org/ magento/project-community-edition:2.4.5 .
   
### 3.2 (1) Latest via Official Composer

Inside `./`

    mkdir '__project'
    
    bin/local create /app/__project
    
### 3.3 (2) Specific via Official Composer

    mkdir '__project'
    
    bin/local cli
    
    cd __project
    
    composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition:2.4.3-p3 ./
 
Enter valid Magento keys

    sudo rsync -azvp __project/ ./ --remove-source-files
    
    sudo rm '__project' -rf

## 4 Start Containers

Inside `./`

    docker-compose up -d
    
Shortcut

    bin/local up    

## 5 Go inside shell container

    docker-compose run --rm deploy
    
Shortcut

    bin/local cli

### 5.1 Install

    bin/magento setup:install --admin-firstname Admin --admin-lastname User --admin-email dominic@xigen.co.uk --admin-user admin --admin-password test123 --base-url http://magento2.docker/ --base-url-secure https://magento2.docker/ --backend-frontname xpanel --db-host db --db-name magento2 --db-user magento2 --db-password magento2 --language en_GB --currency GBP --timezone UTC --use-rewrites 1 --session-save files --use-secure 1 --use-secure-admin 1 --elasticsearch-host elasticsearch --elasticsearch-port 9200
    
2.4.6 opensearch

    bin/magento setup:install --admin-firstname Admin --admin-lastname User --admin-email dominic@xigen.co.uk --admin-user admin --admin-password test123 --base-url http://magento2.docker/ --base-url-secure https://magento2.docker/ --backend-frontname xpanel --db-host db --db-name magento2 --db-user magento2 --db-password magento2 --language en_GB --currency GBP --timezone UTC --use-rewrites 1 --session-save files --use-secure 1 --use-secure-admin 1 --opensearch-host opensearch --opensearch-port 9200

### 5.2 Disable 2FA

    bin/magento module:disable "Magento_TwoFactorAuth"
    
Outside shell container

    bin/local magento module:disable Magento_TwoFactorAuth
    
2.4.6

    bin/magento module:disable Magento_TwoFactorAuth Magento_AdminAdobeImsTwoFactorAuth
    
Outside shell container

    bin/local magento module:disable Magento_TwoFactorAuth Magento_AdminAdobeImsTwoFactorAuth 

## 6 Outside shell container

#### Frontend

    https://magento2.docker/

#### Backend

    https://magento2.docker/xpanel

    admin / test123

## 7 Additional

SMTP extension config

  - host: `mailhog`
  - port: `1025`
  - protocol: `none`
  - authentication: `plain`
  - username/password: `[blank]`
  
## 8 Additional Helper script

In `./` outside container

    bin/local
   
```   
Arguments:
  up                Create and start containers
  down              Destroy containers
  init              Destroy, re-create and start containers and volumes
  
  pull              Pull latest images
  stop              Stop containers
  start             Start containers
  restart           Restart containers

  build             Deployment process
  cachedev          Development cache settings
  cacheflush        Flush cache
  cacheon           All cache on
  cacheoff          All cache off
  cli               Connect to bash
  cron              Run cron
  db                Connect to db
  di                Run di compile
  magento           Run Magento command
  theme             Run theme compilation
  upgrade           Run upgrade command
  composer          Run composer command
  create            Run create project command
```
Example

    bin/local composer require dominicwatts/faker dominicwatts/magentodevelopbundle
    
    bin/local cacheflush
    
    bin/local upgrade
    
    bin/local magento
    
If you have error running local try dos2unix
 
    sudo apt-get install dos2unix

    dos2unix ./bin/local
