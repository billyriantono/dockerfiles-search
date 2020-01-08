FROM centos:7

# Update image, install epel and tools
RUN yum install -y epel-release yum-utils ssh git curl epel-release && yum clean all -y

# Install Remi PHP v7.3
RUN rpm -ivh http://rpms.remirepo.net/enterprise/remi-release-7.rpm && \
  yum install -y \
    php73 \
    php73-php \
    php73-php-bcmath \
    php73-php-cli \
    php73-php-common \
    php73-php-dba \
    php73-php-enchant \
    php73-php-fpm \
    php73-php-gd \
    php73-php-gmp \
    php73-php-imap \
    php73-php-interbase \
    php73-php-intl \
    php73-php-json \
    php73-php-ldap \
    php73-php-mbstring \
    php73-php-mcrypt \
    php73-php-mysqlnd \
    php73-php-opcache \
    php73-php-pdo \
    php73-php-pear \
    php73-php-pecl-apcu \
    php73-php-pecl-gearman \
    php73-php-pecl-igbinary \
    php73-php-pecl-imagick \
    php73-php-pecl-memcached \
    php73-php-pecl-memcache \
    php73-php-pecl-mongodb \
    php73-php-pecl-oauth \
    php73-php-pecl-redis \
    php73-php-pecl-yaml \
    php73-php-pecl-zip \
    php73-php-pgsql \
    php73-php-phalcon3 \
    php73-php-phpiredis \
    php73-php-process \
    php73-php-pspell \
    php73-php-recode \
    php73-php-smbclient \
    php73-php-snappy \
    php73-php-snmp \
    php73-php-soap \
    php73-php-tidy \
    php73-php-xmlrpc \
    php73-php-xml \
    php73-php-pecl-ssh2 && \
  yum clean all -y

# override php.ini
ADD php.ini /etc/opt/remi/php73/php.ini
