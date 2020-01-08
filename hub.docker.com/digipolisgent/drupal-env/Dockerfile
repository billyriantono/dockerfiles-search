FROM php:7.1.9-apache

# Install the gentgrp certificate.
COPY gentgrp.crt /usr/local/share/ca-certificates/
RUN update-ca-certificates

# Install some packages.
RUN apt-get update \
  && apt-get install -y bundler vim curl git unzip libssl-dev libreadline-dev zlib1g-dev gnupg2 \
  && curl -sL https://deb.nodesource.com/setup_8.x | bash - \
  && apt-get install nodejs

# Install some additional PHP modules.
RUN set -ex \
  && buildDeps=' \
    libjpeg62-turbo-dev \
    libpng-dev \
    libpq-dev \
  ' \
  && apt-get install -y --no-install-recommends $buildDeps \
  && rm -rf /var/lib/apt/lists/* \
  && docker-php-ext-configure gd --with-jpeg-dir=/usr --with-png-dir=/usr \
  && docker-php-ext-install -j "$(nproc)" gd mbstring pdo pdo_mysql pdo_pgsql zip \
  && apt-mark manual libjpeg62-turbo libpq5 \
  && apt-get purge -y --auto-remove $buildDeps

# Install ruby-build and some rubies.
WORKDIR /usr/local/src
RUN git clone https://github.com/rbenv/ruby-build.git \
  && PREFIX=/usr/local ./ruby-build/install.sh \
  && ruby-build 1.9.3-p551 /opt/rubies/1.9.3 \
  && ruby-build 2.1.9 /opt/rubies/2.1.9 \
  && ruby-build 2.2.5 /opt/rubies/2.2.5 \
  && ruby-build 2.3.0 /opt/rubies/2.3.0

# Install chruby.
RUN curl -L -o chruby-0.3.9.tar.gz https://github.com/postmodern/chruby/archive/v0.3.9.tar.gz \
  && tar -xzvf chruby-0.3.9.tar.gz \
  && rm chruby-0.3.9.tar.gz \
  && cd chruby-0.3.9 \
  && make install \
  && ./scripts/setup.sh

# Install composer.
WORKDIR /usr/local/bin
RUN php -r "copy('https://raw.githubusercontent.com/composer/getcomposer.org/c1ad3667731e9c5c1a21e5835c7e6a7eedc2e1fe/web/installer', 'composer-setup.php');" \
  && php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
  && php composer-setup.php \
  && php -r "unlink('composer-setup.php');" \
  && mv composer.phar composer

# Install Drush.
WORKDIR /usr/local/composer
RUN composer require drush/drush:^8.0 \
  && ln -s /usr/local/composer/vendor/bin/drush /usr/local/bin/drush

# Install and patch Phing.
RUN composer require phing/phing:^2.0 \
  && ln -s /usr/local/composer/vendor/bin/phing /usr/local/bin/phing \
  && sed -i -e 's#passthru($this->realCommand, $return);#passthru("/bin/bash -c " . escapeshellarg("source /etc/profile.d/chruby.sh; " . $this->realCommand), $return);#g' vendor/phing/phing/classes/phing/tasks/system/ExecTask.php \
  && sed -i -e 's#exec($this->realCommand, $output, $return);#exec("/bin/bash -c " . escapeshellarg("source /etc/profile.d/chruby.sh; " . $this->realCommand), $output, $return);#g' vendor/phing/phing/classes/phing/tasks/system/ExecTask.php

# Install phploc.
WORKDIR /usr/local/phploc
RUN composer require phploc/phploc

# Install phpmd.
WORKDIR /usr/local/phpmd
RUN composer require phpmd/phpmd

# Install phpcpd.
WORKDIR /usr/local/phpcpd
RUN composer require sebastian/phpcpd

# Enable Apache's rewrite module.
RUN a2enmod rewrite
