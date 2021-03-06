FROM ubuntu:14.04

# Install base packages
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && \
    apt-get -yq upgrade && \
    apt-get -yq install \
        mysql-client \
        apache2 \
        libapache2-mod-php5 \
        php5-apcu \
        php5-cli \
        php5-curl \
        php5-gd \
        php5-mcrypt \
        php5-mongo \
        php5-mysql \
        php5-intl \
        php5-json \
        php5-xsl \
	php5-memcache \
	php-apc \
	php-soap \
	php5-imap \
	php-pear \
	php5-dev \
	collectd \
        git curl zip unzip vim wget && \
    rm -rf /var/lib/apt/lists/*

ENV PATH $PATH:/usr/local/composer/vendor/bin
    
# Add apache default vhost configuration
ADD default-vhost.conf /etc/apache2/sites-available/000-default.conf

ADD set_data_permissions.sh /
ADD install_xdebug.sh /
ADD set_debug.sh /
ADD php.ini /etc/php5/apache2/php.ini
ADD debug_php.ini /etc/php5/apache2/debug_php.ini
ADD my.cnf /etc/mysql/my.cnf
ADD 000-default.conf /etc/apache2/sites-enabled/000-default.conf
ADD apache2.conf /etc/apache2/apache2.conf
RUN /install_xdebug.sh && mkdir /tmp/xdebug_profiling
ADD collectd.conf /collectd.conf

# Enable apache modules
RUN a2enmod rewrite php5 vhost_alias headers unique_id

# Enable php modules
RUN php5enmod apcu curl gd mcrypt mongo mysql intl json imap xsl overrides/99

# Install composer and drush
RUN export COMPOSER_HOME=/usr/local/composer && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    composer global require drush/drush:dev-master && \
    composer global install && \
    composer selfupdate && \
    composer global require phpunit/phpunit "3.*" && \
    composer global require phpunit/phpunit-story && \
    composer global require phpunit/php-invoker && \
    composer global require phpunit/dbunit "1.3.2" && \
    composer global require phpunit/phpunit-selenium "1.4.2" && \
    composer global require symfony/yaml && \
    ln -s /usr/local/composer/vendor/drush/drush/drush /usr/local/bin/drush

# Install dockerize
RUN curl -sSL https://github.com/jwilder/dockerize/releases/download/v0.0.2/dockerize-linux-amd64-v0.0.2.tar.gz | tar -C /usr/local/bin -xzf -

# Add run file
ADD apache-run-kube.sh /apache-run-kube.sh
RUN chmod 0500 /apache-run-kube.sh

# from zurmo_config
ADD config /zurmo/zurmo/app/protected/config
ADD conf.d /etc/confd/apache/conf.d
ADD templates /etc/confd/apache/templates

# from zurmo_application
ADD zurmo /zurmo/zurmo
ADD index.php /zurmo/index.php

RUN chown -R www-data /zurmo

# from


VOLUME /var/log/apache2
VOLUME /var/log/collectd

EXPOSE 80
CMD ["/apache-run-kube.sh"]
