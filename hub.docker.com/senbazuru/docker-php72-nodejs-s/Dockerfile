FROM circleci/php:7.2
MAINTAINER senbazuru

RUN deps='\
         ruby \
         nodejs \
         libpq-dev \
         libxml2-dev \
         ' \
    && set -x \
    && curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash - \
    && sudo apt update -qq \
    && sudo apt install -y -qq --no-install-recommends $deps \
    && sudo rm -rf /var/lib/apt/lists/* \
    && sudo gem install bundler hub --no-document \
    && sudo docker-php-ext-install pdo_pgsql soap \
    && composer global require hirak/prestissimo

