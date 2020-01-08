FROM php:7.3-apache

# Ssytem packages
RUN apt-get update \
    && apt-get install -y \
    build-essential \
    gnupg \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    libzip-dev \
    curl \
    lsb-release \
    libonig-dev \
    apt-utils \
    libssl-dev \
    libcurl4-openssl-dev \
    libicu-dev \
# Enable apache modules
	&& a2enmod rewrite headers \
# PHP extensions
	&& docker-php-ext-install pdo_mysql mbstring sockets \
# composer
	&& curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
# Google chrome
	&& curl 'https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb' --output google-chrome-stable_current_amd64.deb \
	&& apt-get -y install ./google-chrome-stable_current_amd64.deb \
	&& ln -s /opt/google/chrome/chrome /bin/chrome \
# Clear apt cache to try and reduce image size
	&& rm -rf /var/lib/apt/lists/*