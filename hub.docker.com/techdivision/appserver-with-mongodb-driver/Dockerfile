FROM appserver/dist:1.1.2

ENV MONGODB_PHP_DRIVER=1.1.8

# Download dependencies and mongodb php driver source
RUN git clone https://github.com/mongodb/mongo-php-driver.git /tmp/mongo-php-driver \
  && cd /tmp/mongo-php-driver \
  && git checkout ${MONGODB_PHP_DRIVER} \
  && git submodule sync \
  && git submodule update --init \
  && apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends autoconf libssl-dev pkg-config

# Compile and install mongodb php driver
RUN cd /tmp/mongo-php-driver \
  && /opt/appserver/bin/phpize \
  && ./configure \
          --with-php-config=/opt/appserver/bin/php-config \
          --prefix=/opt/appserver \
          --with-libdir=lib \
  && make all -j 5 \
  && make install \
  && echo extension=mongodb.so > /opt/appserver/etc/conf.d/mongodb.ini

# Clean up
RUN apt-get purge -y autoconf libssl-dev pkg-config gcc gcc+ make \
  && apt-get clean -y \
  && apt-get autoclean -y \
  && apt-get autoremove -y \
  && rm -rf /var/lib/apt/lists/* \
            /tmp/* \
            /var/tmp/* \
            /var/cache/*
