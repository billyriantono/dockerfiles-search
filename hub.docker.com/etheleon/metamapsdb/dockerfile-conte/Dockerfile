# Dockerfile is used by Docker to build the Docker image
# docker build -t <container_name> .
# For this project docker build -t ekc-cms .
# Ignored when starting the app directly (i.e. $ php artisan serve)

# The Dockerfile needs to be kept up to date with app.prod.docker in
# the docker-image branch so docker.com can build the docker image.

# For development using the dockerfiles, copy the contents of
# deploy/ekc-cms/app.dev.docker to Dockerfile and the contents of
# deploy/ekc-cms/docker-compose.dev.yml into docker-compose.yml

# Provides php to the project
FROM php:7.3.6-fpm

# Create app directory and make it the working directory
RUN mkdir -p /var/www/html
WORKDIR /var/www/html

# Install php dependencies and git
RUN apt-get update
RUN apt-get install -y libmcrypt-dev mysql-client libmagickwand-dev --no-install-recommends
RUN apt-get install -y wget git-all zip unzip vim
RUN pecl install imagick \
    && pecl install mcrypt-1.0.2 \
    && docker-php-ext-enable imagick \
    && docker-php-ext-enable mcrypt \
    && docker-php-ext-install pdo_mysql

# Bundle app source (Excluding /vendor, /node_modules, and docker files)
COPY . /var/www/html

# ******* Install the latest version of composer *******
# ******* https://getcomposer.org/doc/faqs/how-to-install-composer-programmatically.md *******
RUN chmod +x ./deploy/composer_install.sh
RUN ./deploy/composer_install.sh
# Install composer packages
RUN composer install

#Install node.js for npm (/node_modules)
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get install -y nodejs
RUN npm install -g npm@5.1.0
RUN npm install

# change ownership of the laravel files
RUN chown -R www-data:www-data  /var/www/html

# Use the production environment and install a unique key
RUN mv .env.prod .env
RUN php artisan key:generate

# Compile all dependencies
RUN npm run prod

RUN chown -R www-data:www-data /var/www/html/storage /var/www/html/public

RUN php artisan route:clear \
    && php artisan config:clear \
    && php artisan cache:clear
