# Docker para Magento

- PHP 7.3
- Magento 2.3.3

# Install Magento
composer create-project --repository=https://repo.magento.com/ magento/project-community-edition <install-directory-name>


## Setup 
bin/magento setup:install \
--base-url=http://localhost:8080 \
--db-host=db \
--db-name=magento \
--db-user=root \
--db-password=root \
--admin-firstname=admin \
--admin-lastname=admin \
--admin-email=admin@admin.com \
--admin-user=admin \
--admin-password=admin123 \
--language=en_US \
--currency=USD \
--timezone=America/Chicago \
--use-rewrites=1 \
--backend-frontname=admin

## Disable Static Files Settings
Stores > Configuration > Advanced > Developer > Sign Static Files (dev_static_sign) – No

OR 

INSERT INTO `core_config_data`(`path`, `value`) VALUES ('dev/static/sign', 0) ON DUPLICATE KEY UPDATE `value` = 0;
bin/magento cache:clean config

## Util

### Show Image Catalog
bin/magento catalog:image:resize

bin/magento setup:upgrade

bin/magento setup:static-content:deploy -f

### PHP Storm
bin/magento dev:urn-catalog:generate .idea/misc.xml

### MSP Dev Tools
https://github.com/magespecialist/mage-chrome-toolbar#magento-chrome-toolbar-for-msp-devtools

### Mage Cache Clean
https://github.com/mage2tv/magento-cache-clean

composer require --dev mage2tv/magento-cache-clean

vendor/bin/cache-clean.js --watch
