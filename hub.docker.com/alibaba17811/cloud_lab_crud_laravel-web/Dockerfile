# Authors (Ali, Sachin, Ram)
# Creating a Dockerfile for Laravel Framework PHP App (php + apache + mysql)

# Take a Base image from the php dockerhub configurable and functional apache webserver.
FROM php:7.2-apache

# Because our base image based on debian linux thats why we run commands with apt-get
# "apt-get update" retrieve information about what packages can be installed and what packages updates are available to current packages from the internet sources.
RUN apt-get update

# Install development packages and dependencies for Laravel Framework
RUN apt-get install -y git zip curl sudo unzip libicu-dev libbz2-dev libpng-dev libjpeg-dev libmcrypt-dev libreadline-dev g++

# Apache configs + Document root settings
# Our base image "php-apache" set document root as "/var/www/html" by default but in our laraval application index.php file exist in public directory, so we need to edit the apache config as well as sites-available.
ENV APACHE_DOCUMENT_ROOT=/var/www/html/public
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

# We also enable mod_rewrite for URL matching rewrite and mod_headers for .htaccess extra headers like Access-Control-Allow-Origin-
RUN a2enmod rewrite headers

# Then add extensions which are mbstring, pdo_mysql etc required for laraval application and mysql database.
RUN docker-php-ext-install bz2 intl iconv bcmath opcache calendar mbstring mysqli pdo_mysql zip

# composer (php package manager)
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer