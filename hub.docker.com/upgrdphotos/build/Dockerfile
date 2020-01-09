FROM php:7.3-stretch
# Clear apt cache
RUN rm -rf /var/lib/apt/lists/*
# Basic dependencies
RUN apt-get update && apt-get install -y apt-utils zip ssh rsync apt-transport-https python python-pip python-yaml libpng-dev libfreetype6-dev libjpeg62-turbo-dev g++ libicu-dev libxml2-dev libgmp-dev libzip-dev libmagickwand-dev libmagickcore-dev gnupg libpq-dev git wget
RUN docker-php-ext-install intl xml gd mbstring gmp dom zip pdo pdo_pgsql pgsql exif
RUN pecl install imagick
RUN docker-php-ext-enable imagick
# Install AWS CLI
RUN pip install awscli
# Install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === 'a5c698ffe4b8e849a443b120cd5ba38043260d5c4023dbf93e1558871f1f07f58274fc6f4c93bcfd858c6bd0775cd8d1') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --install-dir=/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"
# Install node
RUN curl -sL https://deb.nodesource.com/setup_13.x | bash -
RUN apt-get install -y nodejs
# Install Yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update
RUN apt-get install -y yarn
# Install gulp
RUN npm install -g gulp-cli
# Install php cs fixer
RUN composer global require friendsofphp/php-cs-fixer
ENV PATH="$PATH:/root/.composer/vendor/bin"
# install lokalise CLI
RUN curl -sfL https://raw.githubusercontent.com/lokalise/lokalise-cli-2-go/master/install.sh | sh
# terraform
RUN curl https://releases.hashicorp.com/terraform/0.12.17/terraform_0.12.17_linux_amd64.zip --output terraform.zip
RUN unzip terraform.zip
RUN mv terraform /usr/local/bin
# packer
RUN curl https://releases.hashicorp.com/packer/1.4.5/packer_1.4.5_linux_amd64.zip --output packer.zip
RUN unzip packer.zip
RUN mv packer /usr/local/bin
# sentry-cli
RUN curl -sL https://sentry.io/get-cli/ | bash
