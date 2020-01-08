FROM ubuntu:18.10
LABEL Maintainer="Sakly Ayoub"
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install software-properties-common -yq
RUN add-apt-repository ppa:ondrej/php -y && \
    apt-get update -y
RUN apt-get install -yq \
    apt-utils \
    curl \
    apache2 \
    php7.2 \
    php7.2-cli \
    php7.2-json \
    php7.2-curl \
    php7.2-fpm \
    php7.2-gd \
    php7.2-ldap \
    php7.2-mbstring \
    php7.2-mysql \
    php7.2-soap \
    php7.2-sqlite3 \
    php7.2-xml \
    php7.2-zip \
    php7.2-intl \
    php-imagick \
    nano \
    graphicsmagick \
    imagemagick \
    ghostscript \
    iputils-ping \
    nodejs \
    npm \
    locales \
    wget \
    openssh-server \
    ssmtp \
    mailutils \
    git \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN apt-get update -y && \
    apt-get install libapache2-mod-php7.2 -y && \
    a2enmod php7.2 && \
    update-alternatives --set php /usr/bin/php7.2 && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    mkdir /ioncube && \
    cd /ioncube && \
    wget http://downloads3.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz && \
    tar xvf ioncube_loaders_lin_x86-64.tar.gz && \
    cp /ioncube/ioncube/ioncube_loader_lin_7.2.so /usr/lib/php/20170718 && \
    echo zend_extension = /usr/lib/php/20170718/ioncube_loader_lin_7.2.so > /etc/php/7.2/cli/php.ini && \
    echo zend_extension = /usr/lib/php/20170718/ioncube_loader_lin_7.2.so > /etc/php/7.2/apache2/conf.d/00-ioncube.ini && \
    rm -rf /ioncube/ioncube/ && \
    locale-gen en_US.UTF-8 en_GB.UTF-8 de_DE.UTF-8 es_ES.UTF-8 fr_FR.UTF-8 it_IT.UTF-8 km_KH sv_SE.UTF-8 fi_FI.UTF-8 && \
    a2enmod rewrite expires && \
    { echo "\nStrictHostKeyChecking no"; } > /etc/ssh/ssh_config && \
    mkdir -p /root/.ssh && \
    wget -O /tmp/phpmyadmin.tar.gz https://files.phpmyadmin.net/phpMyAdmin/4.8.2/phpMyAdmin-4.8.2-all-languages.tar.gz && \
    tar xfvz /tmp/phpmyadmin.tar.gz -C /var/www && \
    ln -s /var/www/phpMyAdmin-4.8.2-all-languages /var/www/phpmyadmin && \
    echo "sendmail_path=sendmail -i -t" >> /etc/php/7.2/apache2/conf.d/php-sendmail.ini && \
    rm /var/www/html/index.html && \
    chown -R www-data:www-data /var/www/html
ADD config.inc.php /var/www/phpMyAdmin-4.8.2-all-languages/
ADD php.ini /etc/php/7.2/apache2/conf.d/
ADD revaliases /etc/ssmtp/revaliases
ADD ssmtp.conf /etc/ssmtp/ssmtp.conf
ADD default.conf /etc/apache2/sites-enabled/000-default.conf
VOLUME /var/www/html
COPY entrypoint.sh /usr/local/bin/
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 80 443 587 25
RUN chmod 544 /var/www/phpMyAdmin-4.8.2-all-languages/config.inc.php && \
    ln -sf /dev/stdout /var/log/apache2/access.log && \
    ln -sf /dev/stderr /var/log/apache2/error.log
CMD ["apache2ctl", "-D", "FOREGROUND"]
