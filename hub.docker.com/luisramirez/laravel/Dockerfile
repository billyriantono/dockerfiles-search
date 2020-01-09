# OS distribution
FROM ubuntu:16.04

# Install php packages
RUN apt-get update && apt-get install -y php php-fpm php-mcrypt php-mysql php-ldap php-mbstring php-dom php-zip php-gd

# Enabling mcrypt
RUN phpenmod mcrypt

# Install more
RUN apt-get -y install nginx openssl curl cron

# Configure cron
COPY crontab /etc/cron.d/crontab
RUN chmod 0644 /etc/cron.d/crontab

# Install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
		php -r "if (hash_file('SHA384', 'composer-setup.php') === 'e115a8dc7871f15d853148a7fbac7da27d6c0030b848d9b3dc09e2a0388afed865e6a3d6b3c0fad45c48e2b5fc1196ae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
		php composer-setup.php && \
		php -r "unlink('composer-setup.php');" && \
		mv composer.phar /usr/local/bin/composer

# Setting up stdout and stderr
RUN ln -sf /dev/stdout /var/log/nginx/access.log && \
		ln -sf /dev/stderr /var/log/nginx/error.log

# Port
EXPOSE 80

# Copy the nginx configuration file
COPY ./nginx.conf /etc/nginx/nginx.conf

# Set the default directory where the command will be executed
WORKDIR /www/laravel

# Run the web server
CMD cron && \
		service php7.0-fpm start && \
		nginx -g "daemon off;"
