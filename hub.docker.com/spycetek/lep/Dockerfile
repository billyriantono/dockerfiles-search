# Create a container based on ubuntu 18.04 with Nginx 1.14 and PHP 7.2.
# Build command example: docker build -t "spycetek/lep:u18.04-1.14-7.2-1" .

FROM ubuntu:18.04

# Prepare for package installation
RUN apt-get update && apt-get -y install apt-utils

# Install Commands and Libraries
# php7.2-curl: for phpunit/phpunit-selenium and mailchimp
# php7.2-dev: for ast used by phan
# php7.2-gd: for generating images
# php7.2-mbstring: for dealing with multi-byte languages
# php7.2-sqlite: for unit testing
# php7.2-xml: for aws-sdk-php and unit testing
# php-pear: for static code analyzer phan
# php-xdebug: for debugging and PhpUnit coverage
# python-pip: to install awscli
# unzip: for composer install
# Add openssh-server if ssh server is needed inside of the container.
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install \
  curl \
  git \
  mysql-client=5.7.* \
  nginx=1.14.* \
  openssh-client \
  php7.2 \
  php7.2-curl \
  php7.2-dev \
  php7.2-gd \
  php7.2-fpm \
  php7.2-mbstring \
  php7.2-mysql \
  php7.2-sqlite \
  php7.2-xml \
  php7.2-zip \
  php-pear \
  php-xdebug \
  python-pip \
  sudo \
  unzip \
  vim \
  wget

# This requires python-pip
RUN pip install awscli

# Install ast for phan
RUN pecl install ast-1.0.0 && \
  echo "extension=ast.so" > /etc/php/7.2/mods-available/spycetek.ini && \
  ln -s /etc/php/7.2/mods-available/spycetek.ini /etc/php/7.2/cli/conf.d/30-spycetek.ini

# Install composer
RUN curl -s https://getcomposer.org/installer | php && \
  mv composer.phar /usr/local/bin/composer

# Install npm for webpack, SCSS, and TypeScript
RUN curl -sL https://deb.nodesource.com/setup_11.x | sudo -E bash - && \
  apt-get install -y nodejs

# Install yarn for multiple package.json installation
# ref: https://yarnpkg.com/en/docs/install#debian-stable
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add - && \
  echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list && \
  apt-get update && apt-get install -y yarn

# Add .ssh/config for web server user
# This config file specifies which ssh key file to be used to git clone from our private repo.
RUN mkdir ~www-data/.ssh
COPY files/ssh_config ~www-data/.ssh/config
RUN chown -R www-data:www-data ~www-data/.ssh

# Configure xdebug
RUN echo "xdebug.remote_enable = 1" >> /etc/php/7.2/mods-available/xdebug.ini && \
  echo "xdebug.remote_host = host.docker.internal" >> /etc/php/7.2/mods-available/xdebug.ini && \
  echo "xdebug.remote_port = 9001" >> /etc/php/7.2/mods-available/xdebug.ini

# Disable xdebug by default because it slows down processing php a lot.
# To enable `phpdismod xdebug` then restart fpm.
RUN phpdismod xdebug

# This container should started with the entry point of infinite process like `tail -f /dev/null`.
# Services should be started outside of Dockerfile since these start up command won't be executed, when the container is restarted.
# service php7.2-fpm start
# service nginx start
