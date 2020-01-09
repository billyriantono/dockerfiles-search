# Builds a base image

FROM phusion/baseimage:0.10.0

ENV DEBIAN_FRONTEND noninteractive

WORKDIR /var/www

########################################################################################################################
### Install dependencies ###############################################################################################
########################################################################################################################

RUN mkdir -p /run/php && \
# Configure repository for PHP 7
    LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php -y && \
# Configure repository for Yarn
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
# Configure repository for NodeJS 8
    curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    apt-get update && \
    apt-get autoremove --purge php5-* && \
    apt-get install -y \
      ca-certificates \
      git \
      unzip \
      nginx \
      yarn \
      php7.2-apcu \
      php7.2-fpm \
      php7.2-intl \
      php7.2-mbstring \
      php7.2-xml \
      php7.2-pgsql && \
    rm -rf /etc/nginx/html /var/www/html && \
# Clean up everything when done
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
# Install composer globally
    curl -L -o /usr/local/bin/composer https://getcomposer.org/download/1.6.3/composer.phar && \
    chmod +x /usr/local/bin/composer

########################################################################################################################
### Tweak default configurations #######################################################################################
########################################################################################################################

# Override nginx base configuration and config modules
COPY nginx/nginx.conf /etc/nginx/nginx.conf
COPY nginx/conf.d /etc/nginx/conf.d
COPY nginx/sites-available /etc/nginx/sites-available

# Add additional config files for syslog-ng
COPY syslog-ng/conf.d /etc/syslog-ng/conf.d

# Add runit entries for php-fpm and nginx
COPY service/php-fpm /etc/service/php-fpm
COPY service/nginx   /etc/service/nginx

# Set the correct user for php-fpm
RUN sed -i "s|log_errors_max_len = 1024|log_errors_max_len = 65536|" /etc/php/7.2/fpm/php.ini && \
    sed -i "s|log_errors_max_len = 1024|log_errors_max_len = 65536|" /etc/php/7.2/cli/php.ini && \
    sed -i "s|;error_log = php_errors.log|error_log = syslog|" /etc/php/7.2/fpm/php.ini && \
    sed -i "s|;error_log = php_errors.log|error_log = syslog|" /etc/php/7.2/cli/php.ini && \
    sed -i "s|error_log = /var/log/php7.2-fpm.log|error_log = syslog|" /etc/php/7.2/fpm/php-fpm.conf && \
    sed -i "s|;catch_workers_output = yes|catch_workers_output = yes|" /etc/php/7.2/fpm/pool.d/www.conf && \
# Make sure syslog-ng is able to handle 64KB log messages
    sed -i 's|bad_hostname("^gconfd$");|bad_hostname("^gconfd$"); log_msg_size(65536);|' /etc/syslog-ng/syslog-ng.conf && \
# Have PHP-FPM inherit envs of the parent process (as we pass them through docker)
    sed -i "s|;clear_env = no|clear_env = no|" /etc/php/7.2/fpm/pool.d/www.conf && \
# Set proper timezone
    sed -i "s|;date.timezone =|date.timezone = UTC|" /etc/php/7.2/fpm/php.ini && \
    sed -i "s|;date.timezone =|date.timezone = UTC|" /etc/php/7.2/cli/php.ini && \
# opcache settings (it is enabled by default)
    echo "opcache.validate_timestamps = 0" >> /etc/php/7.2/mods-available/opcache.ini && \
    echo "opcache.max_accelerated_files = 32531" >> /etc/php/7.2/mods-available/opcache.ini && \
# Enable apc for cli
    echo "apc.enable_cli=true" >> /etc/php/7.2/mods-available/apcu_bc.ini
