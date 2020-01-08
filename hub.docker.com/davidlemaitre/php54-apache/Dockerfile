FROM davidlemaitre/base
MAINTAINER David Lemaitre

# Install dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    imagemagick \
    apache2 \
    mysql-client \
    php5 \
    php5-common \
    php5-curl \
    php5-mysql \
    php5-mcrypt \
    php5-gd \
    php5-cli \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Set up the Apache environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

# Enable Apache mods
RUN a2enmod rewrite alias headers expires

# Enable SSL
RUN a2enmod ssl && a2ensite default-ssl

# Set default ServerName
RUN echo ServerName $HOSTNAME > /etc/apache2/conf.d/fqdn

# Default working directory
WORKDIR /var/www/html

# Expose ports
EXPOSE 80 443

# Default command for container
CMD ["/usr/sbin/apache2ctl", "-DFOREGROUND"]
