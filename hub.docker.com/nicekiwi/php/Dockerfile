FROM php:7.2

RUN apt-get update && apt-get install -y apt-utils git zip unzip curl zlib1g-dev libsodium-dev

## Install XDebug
RUN pecl install xdebug-2.7.0
RUN docker-php-ext-enable xdebug

# Install PECL extensions
RUN docker-php-ext-install -j$(nproc) bcmath mysqli zip sodium

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

# Add new user with non-root powers
RUN useradd --system --create-home --home-dir /home/noot --shell /bin/bash --uid 1000 noot

# Switch to new user
USER noot

# Set work dir to new users home dir
WORKDIR /home/noot

# Install Composer paralell downloader
RUN composer global require hirak/prestissimo --no-plugins --no-scripts

# Install Laravel Installer
RUN composer global require laravel/installer --no-plugins --no-scripts

# Add Composer bin to PATH
RUN echo 'export PATH="$PATH:$HOME/.composer/vendor/bin"' >> ~/.bashrc