FROM eclipse/php

USER root

RUN apt-get purge -y php.* && \
    add-apt-repository -y ppa:ondrej/php && \
    apt-get update && \
    apt-get install -y \
    php7.2 \
    php7.2-curl \
    php7.2-mysql \
    php7.2-gd \
    libapache2-mod-php7.2 \
    php7.2-cli \
    php7.2-json \
    php7.2-cgi \
    php7.2-sqlite3 \
    php7.2-dom \
    php7.2-mbstring \
    php7.2-xml \
    git \
    nano \
    vim \
    dos2unix \
    ruby-full \
    build-essential \
    rubygems && \
    gem install sass && \
    echo "phpmyadmin phpmyadmin/dbconfig-install boolean false" | debconf-set-selections && \
    echo "phpmyadmin phpmyadmin/reconfigure-webserver multiselect apache2" | debconf-set-selections && \
    apt-get install -y phpmyadmin && \
    sed -i -e "s/\/\/ \$cfg\['Servers']\[\$i]\['AllowNoPassword'] = TRUE;/\$cfg\['Servers']\[\$i]\['AllowNoPassword'] = TRUE;/g" /etc/phpmyadmin/config.inc.php && \
    rm -rf /usr/share/phpmyadmin/* && \
    wget https://www.phpmyadmin.net/downloads/phpMyAdmin-latest-all-languages.tar.gz -P /usr/share/ && \
    tar -xf /usr/share/phpMyAdmin-latest-all-languages.tar.gz -C /usr/share/phpmyadmin/ --strip 1 && \
    rm -rf /usr/share/phpMyAdmin-latest-all-languages.tar.gz && \
    mkdir /usr/share/phpmyadmin/tmp && \
    chown www-data:www-data /usr/share/phpmyadmin/tmp && \
    sed -i -e "s/define('CONFIG_DIR', '');/define('CONFIG_DIR', '\/etc\/phpmyadmin\/');/g" /usr/share/phpmyadmin/libraries/vendor_config.php && \
    apt-get -y autoremove && \
    apt-get -y clean
    
USER user