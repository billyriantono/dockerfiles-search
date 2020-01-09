FROM php:7.1.11-cli-jessie

# Install system dependencies
RUN apt-get update
RUN apt-get -qq install libpng-dev libfreetype6-dev libjpeg-dev git zip

# Install PHP extensions
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install mysqli gd zip

# Install Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('SHA384', 'composer-setup.php') === '93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --filename=composer --install-dir/bin
RUN php -r "unlink('composer-setup.php');"

# Add possibility to have only one ssh agent running, to be
# able to save ssh key passwords to use in multiple sessions
RUN mkdir /synced_ssh_agent
COPY run_ssh_agent.sh /synced_ssh_agent/

# Define working directory.
WORKDIR /app