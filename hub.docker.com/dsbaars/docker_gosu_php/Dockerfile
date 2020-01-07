FROM php:5.6-fpm
MAINTAINER Djuri Baars <dsbaars@gmail.com>

COPY bin/* /usr/local/bin/
RUN mkdir -p /usr/local/etc/php/disabled

# Install useful extensions
RUN apt-install \
      acl \
      curl \
      g++ \
      git-core \
      libcurl4-openssl-dev \
      libfreetype6-dev \
      libjpeg62-turbo-dev \
      libmcrypt-dev \
      libpng12-dev \
      libpq-dev \
      libssl-dev \
      libxml2-dev libbz2-dev \
      wget \
      zlib1g-dev libicu-dev \
  && docker-php-ext-install \
      mcrypt \
      mysqli \
      pdo_mysql \
      mbstring \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install iconv mcrypt \
  && docker-php-ext-configure intl \
  && docker-php-ext-install gd  \
  && docker-php-ext-install mbstring \
  && docker-php-ext-install intl \
  && docker-php-ext-install calendar \
  && docker-php-ext-install zip \
  && docker-php-ext-install bcmath \
  #&& docker-php-ext-install fileinfo \
  #&& docker-php-ext-install curl \
  #&& docker-php-ext-install json \
  && docker-php-ext-install opcache \
  && docker-php-ext-install pdo_pgsql \
  && docker-php-ext-install pdo_mysql \
  && docker-php-ext-install pcntl
  #&& docker-php-ext-install simplexml \
  #&& docker-php-ext-install xml
RUN docker-php-pecl-install uploadprogress

RUN apt-install zlib1g-dev libicu-dev g++ && \
    docker-php-ext-configure intl && \
    docker-php-ext-install intl && \
    apt-purge g++

# Grab gosu for easy step-down from root
ENV GOSU_VERSION 1.10
RUN set -x \
	&& apt-get install -y --no-install-recommends ca-certificates wget && rm -rf /var/lib/apt/lists/* \
	&& dpkgArch="$(dpkg --print-architecture | awk -F- '{ print $NF }')" \
	&& wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$dpkgArch" \
	&& wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$dpkgArch.asc" \
	&& export GNUPGHOME="$(mktemp -d)" \
	&& gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
	&& gpg --batch --verify /usr/local/bin/gosu.asc /usr/local/bin/gosu \
	&& rm -r "$GNUPGHOME" /usr/local/bin/gosu.asc \
	&& chmod +x /usr/local/bin/gosu \
	&& gosu nobody true \
	&& apt-get purge -y --auto-remove wget

# Include composer
RUN apt-install git rsync zlib1g-dev && \
    docker-php-ext-install zip

ENV COMPOSER_HOME /var/www/.composer
ENV COMPOSER_VERSION 1.4.1
ENV PATH vendor/bin:$COMPOSER_HOME/vendor/bin:$PATH

RUN curl -sS https://getcomposer.org/installer | php -- \
      --install-dir=/usr/local/bin \
      --filename=composer \
      --version=${COMPOSER_VERSION}

RUN mkdir -p $COMPOSER_HOME/cache && \
    chown -R www-data:www-data /var/www && \
    echo "phar.readonly = off" > /usr/local/etc/php/conf.d/phar.ini
VOLUME $COMPOSER_HOME/cache


# Add configs
COPY etc/*.ini /usr/local/etc/php/
RUN cd /usr/local/etc/php && cp php.ini conf.d/environment.ini
RUN sed -i -e '/^access.log/ s/^/;/' /usr/local/etc/php-fpm.d/docker.conf && \
    sed -i -e "s/^pm = dynamic/pm = ondemand/" /usr/local/etc/php-fpm.d/www.conf


# Add entrypoint
COPY init.d /docker-entrypoint-init.d/
COPY docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["php-fpm"]
