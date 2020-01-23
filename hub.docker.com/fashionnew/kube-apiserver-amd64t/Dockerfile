
# Custom Base
FROM faridanthony/docker-ubuntu16-base

# Define Maintainer
MAINTAINER Farid Anthony <farid.anthony@gmail.com>

# Let the conatiner know that there is no tty
ENV DEBIAN_FRONTEND noninteractive

# Setup Environment
ENV TIMEZONE                America/New_York
ENV PHP_MEMORY_LIMIT        512M
ENV MAX_UPLOAD              50M
ENV PHP_MAX_FILE_UPLOAD     200
ENV PHP_MAX_POST            100M
ENV MYSQL_USER              root
ENV MYSQL_PASS              root

# Add application repository URL to the default sources
RUN sed -i 's/^#\s*\(deb.*universe\)$/\1/g' /etc/apt/sources.list 

# Add PHP & NGINX Apt repositories
RUN add-apt-repository -y ppa:ondrej/php && \
    add-apt-repository -y ppa:nginx/stable && \
    apt-get update

# Install specific packages
RUN apt-get update && \
    apt-get install -yq --no-install-suggests --no-install-recommends \
    libpcre3-dev \
    nginx \
    mysql-server-5.7 \ 
    mysql-client-5.7 \
    redis-server \
    supervisor 

# Install PHP packages    
RUN apt-get install -yq --no-install-suggests --no-install-recommends \
    php7.0 \
    php7.0-fpm \
    php7.0-opcache \
    php7.0-dom \
    php7.0-xml \
    php7.0-xmlreader \
    php7.0-ctype \
    php7.0-ftp \
    php7.0-gd \
    php7.0-json \
    php7.0-posix \
    php7.0-curl \
    php7.0-pdo \
    php7.0-sockets \
    php7.0-mcrypt \
    php7.0-mysqli \
    php7.0-sqlite3 \
    php7.0-bz2 \
    php7.0-phar \
    php7.0-zip \
    php7.0-calendar \
    php7.0-iconv \
    php7.0-imap \
    php7.0-dev \
    php7.0-redis \
    php7.0-mbstring \
    php7.0-xdebug \
    php7.0-exif \
    php7.0-xsl \
    php7.0-ldap \
    php7.0-bcmath \
    php7.0-memcached

# Tune up PHP
# Set timezone
RUN echo $TIMEZONE > /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata
RUN sed -i "s|^;date.timezone =.*|date.timezone = $TIMEZONE|" /etc/php/7.0/fpm/php.ini && \
    sed -i "s|memory_limit =.*|memory_limit = ${PHP_MEMORY_LIMIT}|" /etc/php/7.0/fpm/php.ini && \
    sed -i "s|;*upload_max_filesize =.*|upload_max_filesize = ${MAX_UPLOAD}|" /etc/php/7.0/fpm/php.ini && \
    sed -i "s|;*max_file_uploads =.*|max_file_uploads = ${PHP_MAX_FILE_UPLOAD}|" /etc/php/7.0/fpm/php.ini && \
    sed -i "s|;*post_max_size =.*|post_max_size = ${PHP_MAX_POST}|" /etc/php/7.0/fpm/php.ini && \
    sed -i "s|;*cgi.fix_pathinfo=.*|cgi.fix_pathinfo= 0|" /etc/php/7.0/fpm/php.ini && \
    mkdir -p /run/php && \
    chown -R www-data:www-data /run/php

# Tune up PHP FPM & Fix ownership of sock file for php-fpm
RUN sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php/7.0/fpm/php-fpm.conf && \
    sed -i '/^listen = /clisten = 0.0.0.0:9000' /etc/php/7.0/fpm/pool.d/www.conf && \
    sed -i '/^listen.allowed_clients/c;listen.allowed_clients =' /etc/php/7.0/fpm/pool.d/www.conf && \
    find /etc/php/7.0/cli/conf.d/ -name "*.ini" -exec sed -i -re 's/^(\s*)#(.*)/\1;\2/g' {} \;

# Setup MySQL
RUN sed -i 's/^\(bind-address\s.*\)/# \0/' /etc/mysql/my.cnf && \
    echo "mysqld_safe &" > /tmp/config && \
    echo "mysqladmin --silent --wait=30 ping || exit 1" >> /tmp/config && \
    echo "mysql -e \"GRANT ALL ON *.* TO root@'%' IDENTIFIED BY 'root' WITH GRANT OPTION; FLUSH PRIVILEGES;\"" >> /tmp/config && \
    bash /tmp/config && \
    rm -f /tmp/config && \
    /etc/init.d/mysql stop # Stop MySQL, we will run this with supervisor

# Setup composer
RUN curl -O https://getcomposer.org/composer.phar && \
    mv composer.phar /usr/local/bin/composer && \
    chmod +x /usr/local/bin/composer

# Setup Phalcon 3
RUN curl -s https://packagecloud.io/install/repositories/phalcon/stable/script.deb.sh | bash && \
    wget https://www.dotdeb.org/dotdeb.gpg && \
    apt-key add dotdeb.gpg && \
    git clone --depth=1 git://github.com/phalcon/cphalcon.git /usr/local/src/cphalcon && \
    cd /usr/local/src/cphalcon/build && ./install; \
    echo "extension=phalcon.so" >> /etc/php/7.0/fpm/conf.d/30-phalcon.ini && \
    echo "extension=phalcon.so" >> /etc/php/7.0/cli/conf.d/30-phalcon.ini

# Setup Nginx
RUN rm -rf /etc/nginx/conf.d/* && rm -rf /etc/nginx/sites-enabled/default
COPY build/nginx/default.conf /etc/nginx/sites-available/default
RUN ln -s /etc/nginx/sites-available/default /etc/nginx/sites-enabled/default

# Setup Supervisor daemon
COPY build/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Setup dirs and permissions
RUN mkdir -p /run/php && \
    chown -R www-data:www-data /var/www && \
    chown -R www-data:www-data /run/php

# Setup test site
COPY build/php/index.php /var/www/index.php
CMD chmod 644 /var/www/index.php

# Clear apt cache and remove unnecessary packages
RUN apt-get autoclean && apt-get -y autoremove && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Expose volumes
VOLUME ["/var/www"]
VOLUME ["/etc/php/7.0/fpm/pool.d"]

# Internal Port Expose
EXPOSE 80 443 3306 9000

# Start Supervisord
CMD ["/usr/bin/supervisord", "-n"]
