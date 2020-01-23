FROM php:7.2-cli

# Let the container know that there is no tty
#ENV DEBIAN_FRONTEND noninteractive
ENV COMPOSER_NO_INTERACTION 1

# Update Distro
RUN apt-get update \
&& apt-get install -my \
wget \
git \
libpng-dev \
gnupg \
jq \
zip \
unzip

# Install Extension
RUN docker-php-ext-install pdo_mysql

# Install Composer
RUN curl -sS https://getcomposer.org/installer \
     -o composer-setup.php \
    && php composer-setup.php \
        --install-dir=/usr/local/bin \
        --filename=composer

# Install Node & NPM
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get install -y nodejs
