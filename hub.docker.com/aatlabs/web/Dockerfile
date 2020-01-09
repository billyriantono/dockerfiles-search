FROM ubuntu:14.04

MAINTAINER @aatlabs

# Install base packages
RUN apt-get update && \
    apt-get install -y \
    pkg-config \
    libcurl3-dev \
    apache2 \
    libapache2-mod-php5 \
    python-setuptools \
    php5-mysql \
    php5-gd \
    php5-curl \
    php-apc \
    php-pear \
    php5-mcrypt \
    php5-memcached \
    curl \
    wget \
    apt-transport-https && \
    rm -rf /var/lib/apt/lists/*

# Newrelic non interactive install (https://docs.newrelic.com/docs/agents/php-agent/advanced-installation/silent-mode-install-script-advanced)
ENV NR_INSTALL_SILENT 1

# Add New Relic Agent
RUN wget -O - https://download.newrelic.com/548C16BF.gpg | apt-key add -
RUN echo "deb http://apt.newrelic.com/debian/ newrelic non-free" > /etc/apt/sources.list.d/newrelic.list
RUN apt-get update && \
    apt-get install -y newrelic-php5
RUN newrelic-install install

# Add Elastic Beats
RUN wget -O - https://packages.elasticsearch.org/GPG-KEY-elasticsearch | apt-key add -
RUN echo "deb https://packages.elastic.co/beats/apt stable main" > /etc/apt/sources.list.d/beats.list
RUN apt-get update && \
    apt-get install filebeat

# Download & Add Elasticache Cluster Client
# Using php-memcached until cluster endpoint issues have been resolved
#RUN wget http://elasticache-downloads.s3.amazonaws.com/ClusterClient/PHP-5.5/latest-64bit -O AmazonElastiCacheClusterClient-1.0.1-PHP55-64bit.tgz
#RUN tar -xvf AmazonElastiCacheClusterClient-1.0.1-PHP55-64bit.tgz
#RUN cp AmazonElastiCacheClusterClient-1.0.0/amazon-elasticache-cluster-client.so /usr/lib/php5/20121212/
#RUN cp AmazonElastiCacheClusterClient-1.0.0/memcached.ini /etc/php5/cli/conf.d/memcached.ini
#RUN echo "extension=/usr/lib/php5/20121212/amazon-elasticache-cluster-client.so" >> /etc/php5/cli/conf.d/memcached.ini
#RUN cp /etc/php5/cli/conf.d/memcached.ini /etc/php5/apache2/conf.d/memcached.ini

# Configure Apache & PHP
RUN a2enmod \
rewrite \
vhost_alias \
headers \
access_compat \
alias \
authz_host \
deflate \
dir \
expires \
mime \
mpm_prefork \
php5 \
ssl \
proxy \
proxy_http \
proxy_connect
COPY config/php.ini /etc/php5/apache2/php.ini
COPY config/apache2.conf /etc/apache2/apache2.conf
COPY config/mpm_prefork.conf /etc/apache2/mods_available/mpm_prefork.conf

# Enable PHP mcrypt module
RUN php5enmod mcrypt

# We will copy newrelic.ini from the application based on environment

RUN touch /var/log/php_errors.log
RUN chown www-data:www-data /var/log/php_errors.log
RUN chmod g+rw /var/log/php_errors.log

# Document that the service listens on port 80
EXPOSE 80
