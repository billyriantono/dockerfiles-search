FROM php:7-cli

Maintainer Bharat Parsiya <bnap00@gmail.com>

RUN echo "memory_limit=-1" > "$PHP_INI_DIR/conf.d/memory-limit.ini" \
&& echo "date.timezone=Asia/Kolkata" > "$PHP_INI_DIR/conf.d/date_timezone.ini"

VOLUME /root/composer
ENV PATH "/composer/vendor/bin:$PATH"
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV COMPOSER_VERSION 1.3.1

# Packages

RUN export GNUPGHOME="$(mktemp -d)" \
    && gpg --keyserver "hkp://pgp.mit.edu" --recv-keys '3050AC3CD2AE6F03' \
    && gpg -a --export --armor '3050AC3CD2AE6F03' | apt-key add - \
    && rm -r "$GNUPGHOME"
    
    
RUN echo "deb http://download.opensuse.org/repositories/home:/rtCamp:/EasyEngine/Debian_8.0/ /" >> /etc/apt/sources.list \
    && apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get \
      -o Dpkg::Options::="--force-confmiss" \
      -o Dpkg::Options::="--force-confold" \
      -y install nginx-custom nginx-ee \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng12-dev \
    libbz2-dev \
    libxslt-dev \
    php-pear \
    php5-mcrypt \
    python-pip \
    curl \
    git \
    subversion \
    unzip \
    wget \
    zip \
    mariadb-server \
    dbus fonts-droid ghostscript groff-base gsfonts libavahi-client3 \
    libavahi-common-data libavahi-common3 libcap-ng0 libcups2 \
    libcupsfilters1 libcupsimage2 libdbus-1-3 libgs9 \
    libgs9-common libijs-0.35 libjbig2dec0 libnetpbm10 \
    libpaper-utils libpaper1 libxaw7 libxmu6 netpbm poppler-data psutils \
  && rm -r /var/lib/apt/lists/*

# PHP Extensions
RUN docker-php-ext-install bcmath mcrypt zip bz2 mbstring pcntl xsl \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install gd \
  && docker-php-ext-install mysqli

# Setup the Composer installer
RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer \
  && curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig \
  && php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }"

# Start MYSQL Service and set root password as root
RUN service mysql start && mysql -e "create database wp" && mysqladmin -u root password root

# Install Composer
RUN php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer --version=${COMPOSER_VERSION} && rm -rf /tmp/composer-setup.php

RUN composer global require deployer/deployer deployer/recipes wp-cli/wp-cli

#install python aws cli for elastic beanstalk
RUN pip install --upgrade pip
RUN pip install awsebcli 
RUN pip install awscli
