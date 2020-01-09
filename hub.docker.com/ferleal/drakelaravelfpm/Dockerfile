FROM php:7.4-fpm

ARG ROOTPWD

ENV USER=drake USER_ID=1000 USER_GID=1000

# Need to modify user on www.conf on /usr/lib/etc/php-fpm.d/www.conf to mydocker
# Also need to force master php-fpm to mydocker user

RUN apt-get update \
  && apt-get install -y --no-install-recommends  \
    apt-utils \
    curl \
    libzip-dev \
    libmemcached-dev \
    libz-dev \
    libpq-dev \
    libwebp-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libfreetype6-dev \
    libssl-dev \
    libgmp-dev \
    unzip \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* 


  # Install the PHP pdo_mysql extention
  RUN docker-php-ext-install pdo_mysql \
  # Install FILEINFO ZIP
  && docker-php-ext-install fileinfo zip \
  # Install Math
  && docker-php-ext-install -j$(nproc) \
		gmp \
		bcmath \
    pcntl \
  # Install the PHP gd library
  && docker-php-ext-configure gd \
  --with-webp   \
  --with-jpeg   \
  --with-freetype  \  
  && docker-php-ext-install gd 


RUN curl -sS https://getcomposer.org/installer | php \
        && mv composer.phar /usr/local/bin/ \
        && ln -s /usr/local/bin/composer.phar /usr/local/bin/composer \
        && groupadd --gid "${USER_GID}" "${USER}" \
        &&  useradd \
      --uid ${USER_ID} \
      --gid ${USER_GID} \
      --create-home \
      --shell /bin/bash \
      ${USER} 

RUN echo "root:$ROOTPWD" | chpasswd

USER ${USER}

ENTRYPOINT ["docker/scripts/app.sh"]

