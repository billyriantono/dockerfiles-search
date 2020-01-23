from ubuntu:18.04

MAINTAINER Yogesh Sharma

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y sudo \
    && apt-get install -y vim \
    && apt-get install -y rsyslog \
    && apt-get install -y software-properties-common \
    && apt-get install -y build-essential \
    && apt-get install -y tcl8.5 \
    && apt-get install -y cron \
    && apt-get install -y curl \
    && apt-get install -y rsync \
    && apt-get install -y git \
    && apt-get install -y psmisc \
    && apt-get install -y apt-transport-https \
    && apt-get install -y supervisor \
    && apt-get install -y lsb \
    && echo "postfix postfix/mailname string root" | debconf-set-selections \
    && echo "postfix postfix/main_mailer_type string No configuration" | debconf-set-selections \
    && apt-get install -y postfix mailutils libsasl2-2 libsasl2-modules \
    && apt-get install -y openssh-server \
    && mkdir /var/run/sshd \
    && sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config \
    && apt-get install -y language-pack-en-base \
    && apt-get update \
    && locale-gen en_US.UTF-8 \
    && export LANG=en_US.UTF-8 \
    && LC_ALL=en_US.UTF-8 \
    && apt-get update \
    && add-apt-repository ppa:ondrej/apache2 \
    && apt-get install -y apache2 \
    && a2enmod rewrite \
    && cd /etc/apache2/conf-available \
    && printf "<Directory "/phpmyadmin">\nAllowOverride all\nRequire all granted\n</Directory>\nAlias /phpmyadmin /phpmyadmin" > phpmyadmin.conf \
    && a2enconf phpmyadmin.conf \
    && apt-get install -y debconf-utils \
    && apt-get -y install mysql-client-5.7 \
    && add-apt-repository ppa:ondrej/php \
    && apt-get update \
    && apt-get install -y php5.6 libapache2-mod-php5.6 php5.6-mysql \
    && apt-get install -y php5.6-cgi php5.6-cli php5.6-curl php5.6-imap php5.6-gd php5.6-pgsql php5.6-sqlite3 php5.6-mbstring php5.6-json \
    && apt-get install -y php5.6-bz2 php5.6-mcrypt php5.6-xmlrpc php5.6-gmp php5.6-xsl php5.6-soap php5.6-xml php5.6-zip php5.6-dba \
    && apt-get update \
    && apt-get install -y libapache2-mod-php7.0 php7.0 php7.0-mysql \
    && apt-get install -y php7.0-common php7.0-gd php7.0-mcrypt php7.0-curl php7.0-intl php7.0-xsl php7.0-soap \
    && apt-get install -y php7.0-mbstring php7.0-zip php7.0-bcmath php7.0-iconv php7.0-imagick \
    && apt-get update \
    && apt-get install -y libapache2-mod-php7.1 php7.1 php7.1-mysql \
    && apt-get install -y php7.1-common php7.1-gd php7.1-mcrypt php7.1-curl php7.1-intl php7.1-xsl php7.1-soap \
    && apt-get install -y php7.1-mbstring php7.1-zip php7.1-bcmath php7.1-iconv php7.1-imagick \
    && apt-get update \
    && apt-get install -y libapache2-mod-php7.2 php7.2 php7.2-mysql \
    && apt-get install -y php7.2-common php7.2-gd php7.2-curl php7.2-intl php7.2-xsl php7.2-soap \
    && apt-get install -y php7.2-mbstring php7.2-zip php7.2-tidy php7.2-bcmath php7.2-iconv php7.2-imagick \
    && apt-get install -y php-xml \
    && a2dismod php5.6 \
    && a2enmod php7.2  \
    && service apache2 restart \
    && apt-get -y install gcc make autoconf libc-dev pkg-config \
    && apt-get -y install libmcrypt-dev \
    && apt-get update \
    && apt-get -y install php-dev libmcrypt-dev php-pear \
    && pecl channel-update pecl.php.net \
    && pecl install mcrypt-1.0.2 \
    && service apache2 restart \
    && apt-get update \
    && apt-get install -y php7.3 php7.3-cli php7.3-common \
    && apt-get install -y php-pear php7.3-curl php7.3-dev php7.3-gd php7.3-mbstring php7.3-zip php7.3-mysql php7.3-xml \ 
    && apt-get install -y libapache2-mod-php7.3 php7.3-imagick php7.3-recode php7.3-tidy php7.3-xmlrpc php7.3-intl \
    && cd / \
    && wget https://files.phpmyadmin.net/phpMyAdmin/4.8.3/phpMyAdmin-4.8.3-english.tar.gz \
    && tar xvzf phpMyAdmin-4.8.3-english.tar.gz \
    && mv phpMyAdmin-4.8.3-english phpmyadmin \
    && rm -rf phpMyAdmin-4.8.3-english.tar.gz \
    && chown -R www-data:www-data phpmyadmin \
    && cp phpmyadmin/config.sample.inc.php phpmyadmin/config.inc.php \
    && curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && chmod +x /usr/local/bin/composer \
#    && curl -L https://packagecloud.io/varnishcache/varnish5/gpgkey | sudo apt-key add - \
#    && echo "deb https://packagecloud.io/varnishcache/varnish5/ubuntu/ xenial main" | sudo tee -a /etc/apt/sources.list.d/varnishcache5.list \
    && apt-get update \
    && apt-get install -y varnish \
    && apt-get install -y redis-server \
    && apt-get install -y vsftpd \
    && apt-get -y update \
    && curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && chmod +x /usr/local/bin/composer \
    && curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash - \
    && apt-get install -y nodejs \
    && npm install -g grunt-cli \
#    && cd / \
#    && wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb \
#    && dpkg -i erlang-solutions_1.0_all.deb \
#    && apt-get -y update \
#    && echo 'deb http://www.rabbitmq.com/debian/ testing main' | sudo tee /etc/apt/sources.list.d/rabbitmq.list \
#    && wget -O- https://www.rabbitmq.com/rabbitmq-release-signing-key.asc | sudo apt-key add - \
#    && apt-get -y update \
#    && apt-get install -y rabbitmq-server
     && service apache2 restart

#Apache Configuration Files
# ADD tools/docker/apache2/ports.conf /etc/apache2/ports.conf
# ADD tools/docker/apache2/apache2.conf /etc/apache2/apache2.conf
# ADD tools/docker/apache2/envvars /etc/apache2/envvars
# ADD tools/docker/apache2/sites-available/000-default.conf /etc/apache2/sites-available/000-default.conf
#PHP Configuration Files
ADD tools/docker/php/php56/apache2/php.ini /etc/php/5.6/apache2/php.ini
ADD tools/docker/php/php56/cli/php.ini /etc/php/5.6/cli/php.ini
ADD tools/docker/php/php70/apache2/php.ini /etc/php/7.0/apache2/php.ini
ADD tools/docker/php/php70/cli/php.ini /etc/php/7.0/cli/php.ini
ADD tools/docker/php/php71/apache2/php.ini /etc/php/7.1/apache2/php.ini
ADD tools/docker/php/php71/cli/php.ini /etc/php/7.1/cli/php.ini
ADD tools/docker/php/php72/apache2/php.ini /etc/php/7.2/apache2/php.ini
ADD tools/docker/php/php72/cli/php.ini /etc/php/7.2/cli/php.ini
ADD tools/docker/php/php73/apache2/php.ini /etc/php/7.3/apache2/php.ini
ADD tools/docker/php/php73/cli/php.ini /etc/php/7.3/cli/php.ini
#PHP Scripts
ADD tools/docker/php/scripts/php56 /usr/bin/php56
ADD tools/docker/php/scripts/php70 /usr/bin/php70
ADD tools/docker/php/scripts/php71 /usr/bin/php71
ADD tools/docker/php/scripts/php72 /usr/bin/php72
ADD tools/docker/php/scripts/php73 /usr/bin/php73
#PHP Script Execute Permission
RUN chmod +x /usr/bin/php56
RUN chmod +x /usr/bin/php70
RUN chmod +x /usr/bin/php71
RUN chmod +x /usr/bin/php72
RUN chmod +x /usr/bin/php73
#Phpmyadmin Configuration Files
ADD tools/docker/phpmyadmin/config.inc.php /phpmyadmin/config.inc.php
#Postfix Configuration Files
ADD tools/docker/postfix/main.cf /etc/postfix/main.cf
#Supervisor Configuration Files
ADD tools/docker/supervisor/supervisord.conf /etc/supervisor/supervisord.conf
ADD tools/docker/supervisor/conf.d/apps.conf /etc/supervisor/conf.d/apps.conf
#Entrypoint Scripts
ADD tools/docker/scripts/entrypoint.sh /entrypoint.sh
ADD tools/docker/scripts/start.sh /start.sh
ADD tools/docker/scripts/user.sh /user.sh

RUN chmod +x /*.sh

EXPOSE 21 22 80 443 8080

ENTRYPOINT ["/bin/bash", "/entrypoint.sh"]
CMD ["/bin/bash", "/start.sh"]
