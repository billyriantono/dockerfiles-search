FROM wezztt/php:7.3-ci-alpine

ENV COMPOSER_HOME /root/.composer
#Code Sniffer
RUN composer global require "squizlabs/php_codesniffer=*"
RUN ln -s /root/.composer/vendor/bin/phpcs /usr/local/bin/phpcs
#Mess Detector
RUN composer global require "phpmd/phpmd=*"
RUN ln -s /root/.composer/vendor/bin/phpmd /usr/local/bin/phpmd
#PHP CS Fixer
RUN composer global require "friendsofphp/php-cs-fixer=*"
RUN ln -s /root/.composer/vendor/bin/php-cs-fixer /usr/local/bin/php-cs-fixer
