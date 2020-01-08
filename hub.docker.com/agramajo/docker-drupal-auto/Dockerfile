FROM drupal:8.6.2

# Install packages
RUN rm /bin/sh && ln -s /bin/bash /bin/sh && \
    apt-get update && apt-get install --no-install-recommends -y \
    curl \
    wget \
    vim \
    git \
    unzip \
    mysql-client

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    ln -s /root/.composer/vendor/bin/drush /usr/local/bin/drush

# Allow Composer to be run as root
ENV COMPOSER_ALLOW_SUPERUSER=1

# Install Drush
RUN composer global require drush/drush && \
    composer global update

# Speed
RUN composer global require hirak/prestissimo

# Apply patch
RUN wget https://www.drupal.org/files/issues/2018-05-25/drupal_core-percona_compliance-2856362-13-8.6.x.patch && \
    patch -p1 < drupal_core-percona_compliance-2856362-13-8.6.x.patch

# Clean repository
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Remove the vanilla Drupal project that comes with the parent image.
RUN rm -rf /var/www/html/*

# Apache config
RUN sed -ri -e 's!/var/www/html!/var/www/html/web!g' /etc/apache2/sites-available/*.conf

