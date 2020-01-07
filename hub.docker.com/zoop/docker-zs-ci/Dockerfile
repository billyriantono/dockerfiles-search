FROM composer/composer:php5

RUN apt-get update -qq

# install npm
RUN apt-get install -y -qq npm bash
RUN ln -s /usr/bin/nodejs /usr/bin/node

# install bower and gulp
RUN npm install --global gulp bower

# Enable PHP intl
RUN apt-get install -y zlib1g-dev libicu-dev g++ jq \
  && docker-php-ext-configure intl \
  && docker-php-ext-install intl

# Fetch Zend CI tools
RUN curl -sSL -o /usr/bin/zs-client.phar https://github.com/zend-patterns/ZendServerSDK/raw/master/bin/zs-client.phar \
  && chmod a+x /usr/bin/zs-client.phar
RUN curl -sSL -o /usr/bin/zfdeploy.phar https://packages.zendframework.com/zf-deploy/zfdeploy.phar \
  && chmod a+x /usr/bin/zfdeploy.phar

# Set correct entrypoint
CMD ["/bin/bash"]
ENTRYPOINT []