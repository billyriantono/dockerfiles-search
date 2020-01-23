FROM php:5.6.27-fpm

ENV DOCKERIZE_VERSION v0.6.1


RUN echo "deb [check-valid-until=no] http://archive.debian.org/debian jessie-backports main" > /etc/apt/sources.list.d/jessie-backports.list \
  && sed -i '/deb http:\/\/deb.debian.org\/debian jessie-updates main/d' /etc/apt/sources.list \
  && apt-get -o Acquire::Check-Valid-Until=false update \
  && apt-get install -y \
    libfreetype6-dev \
    libicu-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng12-dev \
    libxslt1-dev \
    git \
    vim \
    wget \
    lynx \
    psmisc \
    yui-compressor \
    jpegoptim \
    optipng \
    cron \
    supervisor \
    libmagickwand-dev \
    bzip2 \
    gifsicle \
    libjpeg-progs \
    optipng \
  && apt-get clean

RUN docker-php-ext-configure \
    gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/; \
  docker-php-ext-install \
    gd \
    intl \
    mbstring \
    mcrypt \
    pdo_mysql \
    xsl \
    zip \
    opcache \
    soap

RUN pecl install imagick \
    && docker-php-ext-enable imagick

# Install Composer
RUN curl -sS https://getcomposer.org/installer | \
    php -- \
      --install-dir=/usr/local/bin \
      --filename=composer \
      --version=1.1.2

# Install Node.js
RUN curl -sL  https://deb.nodesource.com/setup_7.x \
    | sed 's|apt-get update|apt-get -o Acquire::Check-Valid-Until=false update|g' \
    | bash - \
    && apt-get install -y nodejs

# Install MageRun
RUN cd /usr/local/bin && \
    wget https://files.magerun.net/n98-magerun.phar && \
    chmod +x ./n98-magerun.phar

# Install Dockerize
RUN curl -Ls https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
           | tar -xzv -C /usr/local/bin