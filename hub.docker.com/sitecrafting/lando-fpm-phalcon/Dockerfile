FROM devwithlando/php:7.2-fpm

LABEL maintainer="Sean Dean <sdean@sitecrafting.com>" license="MIT"

# Configure PHP to include Phalcon module
COPY phalcon.ini .

# Install Phalcon
RUN git clone --depth=1 git://github.com/phalcon/cphalcon.git /cphalcon \
  && cd /cphalcon/build \
  && ./install \
  && /usr/local/bin/docker-php-ext-enable phalcon
