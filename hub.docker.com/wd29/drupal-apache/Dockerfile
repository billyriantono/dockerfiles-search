FROM phusion/baseimage
MAINTAINER Benjamin Favre <ben@webdesign29.net>

ENV HOME=/root/ DHLEVEL=2048 COMPOSER_HOME=/var/www/html/ DRUSH_VERSION=8.0.5 DRUPAL_CONSOLE_VERSION=1.0.0-alpha1
RUN echo /var/www/ > /etc/container_environment/HOME && \
    echo 2048 > /etc/container_environment/DHLEVEL && \
    echo /var/www/html/ > /etc/container_environment/COMPOSER_HOME

RUN export DEBCONF_NONINTERACTIVE_SEEN=true DEBIAN_FRONTEND=noninteractive && \
    echo "Europe/Paris" > /etc/timezone; dpkg-reconfigure tzdata && \
    apt-get -qy update && apt-get -qy upgrade && locale-gen fr_FR.UTF-8 && export LANG=fr_FR.UTF-8 && export LANGUAGE=fr_FR:fr && export LC_ALL=fr_FR.UTF-8 && \
	apt-get -qy install build-essential vim python-setuptools nano curl iputils-ping wget mysql-client software-properties-common --fix-missing && \
	add-apt-repository ppa:ondrej/php && \
	curl -sL https://deb.nodesource.com/setup_6.x | bash - && \
	apt-get -qy update && apt-get -qy install git make re2c nodejs libpcre3-dev libmemcached-dev pkg-config zip --fix-missing && \
	apt-get -qy --force-yes install php7.0-fpm php7.0-curl php7.0-cli php7.0-xml php7.0-cgi php7.0-common php7.0-json php7.0-opcache \
	php7.0-mysql php7.0-phpdbg php7.0-gd php7.0-apcu php7.0-imap php7.0-ldap php7.0-pgsql php7.0-pspell php7.0-recode \
	php7.0-mcrypt php7.0-tidy php7.0-zip php7.0-dev php7.0-mbstring php7.0-intl php7.0-gd && \
	apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/* && \
    rm -rf /var/tmp/*


#Add more for php7 extension
ADD php7/mods-available/*.ini /etc/php/7.0/mods-available/
ADD php7/lib/*.so /usr/lib/php/20151012/
RUN phpenmod memcached && phpenmod redis

#ulimit tool
RUN touch /usr/bin/getulimit && \
    chmod 777 /usr/bin/getulimit  && \
    echo "#!/bin/bash" >> /usr/bin/getulimit && \
    echo "ulimit -Ha" >> /usr/bin/getulimit

#ssh service (remove phusion restriction)
RUN rm -f /etc/service/sshd/down
RUN ssh-keygen -q -t rsa -N '' -f /root/.ssh/id_rsa

# Add colours to bashrc
RUN  sed -i -e "s/#force_color_prompt=yes/force_color_prompt=yes/g" /root/.bashrc

# Install SSH daemon configuration
ADD ./etc/sshd/sshd_config /etc/ssh/sshd_config

# Add deploy key
RUN mkdir -p /root/.ssh
COPY ./deploy_key /root/.ssh/deploy_key
RUN chmod 600 /root/.ssh/deploy_key

# Configure SSH to use deploy key for Github and Bitbucket
COPY ./config/ssh/config /root/.ssh/config

# Add docker_key as authorized key for ssh login
ADD docker_key.pub /tmp/docker_key.pub
RUN cat /tmp/docker_key.pub >> /root/.ssh/authorized_keys && rm -f /tmp/docker_key.pub
RUN chmod 0600 /root/.ssh/authorized_keys


# Configure PHP (FPM)
RUN sed -i "s/display_errors = .*/display_errors = stderr/" /etc/php/7.0/fpm/php.ini && \
    sed -i "s/memory_limit = .*/memory_limit = 2048M/" /etc/php/7.0/fpm/php.ini && \
    sed -i "s/;date.timezone.*/date.timezone = Europe\/Paris/" /etc/php/7.0/fpm/php.ini && \
    sed -i "s/max_execution_time = .*/max_execution_time = 300/" /etc/php/7.0/fpm/php.ini && \
    sed -i "s/max_input_time = .*/max_input_time = 300/" /etc/php/7.0/fpm/php.ini && \
    sed -i "s/post_max_size = .*/post_max_size = 128M/" /etc/php/7.0/fpm/php.ini && \
    sed -i "s/upload_max_filesize = .*/upload_max_filesize = 128M/" /etc/php/7.0/fpm/php.ini && \
    sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathi nfo=0/" /etc/php/7.0/fpm/php.ini && \
    sed -i 's|memory_limit = 128M|memory_limit = 256M|g' /etc/php/7.0/fpm/php.ini

# Configure PHP (CLI)
RUN sed -i "s|;cgi.fix_pathinfo=1|cgi.fix_pathinfo=0|" /etc/php/7.0/cli/php.ini && \
	sed -i "s|;date.timezone =.*|date.timezone = Europe/Paris|" /etc/php/7.0/cli/php.ini && \
	sed -i 's|memory_limit = 128M|memory_limit = 512M|g' /etc/php/7.0/cli/php.ini

# Force PHP in Foreground
RUN sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php/7.0/fpm/php-fpm.conf

# Change pool config to use port instead of socket
RUN sed -i '/^listen = /clisten = 127.0.0.1:9000' /etc/php/7.0/fpm/pool.d/www.conf && \
    sed -i '/^;listen.owner/clisten.owner = www-data' /etc/php/7.0/fpm/pool.d/www.conf && \
    sed -i -e '/^;listen.group = www-data/clisten.group = www-data' /etc/php/7.0/fpm/pool.d/www.conf && \
    sed -i -e '/^;listen.mode = www-data/clisten.mode = 0660' /etc/php/7.0/fpm/pool.d/www.conf

# Apache
RUN add-apt-repository 'deb http://eu.archive.ubuntu.com/ubuntu/ trusty multiverse' && \
    add-apt-repository 'deb http://eu.archive.ubuntu.com/ubuntu/ trusty-updates multiverse' && \
    apt-get update && \
    DEBIAN_FRONTEND="noninteractive" apt-get install --yes \
        apache2                 \
        libapache2-mod-fastcgi  \
        ssl-cert
RUN a2dissite 000-default
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
RUN cp /etc/apache2/conf-available/php7.0-fpm.conf /etc/apache2/conf-available/php7.0-fpm.conf.bak
COPY ./config/apache2/conf-available/php7.0-fpm.conf /etc/apache2/conf-available/php7.0-fpm.conf
RUN cp -r /etc/apache2/sites-available /etc/apache2/sites-available.bak
COPY ./config/apache2/sites-available /etc/apache2/sites-available
RUN cp -r /etc/apache2/apache2.conf /etc/apache2/apache2.back
COPY ./config/apache2/apache2.conf /etc/apache2/apache2.conf
RUN a2enmod     \
    actions     \
    headers     \
    rewrite
RUN a2enconf php7.0-fpm
RUN a2ensite default

# Install composer
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer

# Install Drush
RUN curl -sSL https://github.com/drush-ops/drush/releases/download/$DRUSH_VERSION/drush.phar -o /usr/local/bin/drush && \
    chmod +x /usr/local/bin/drush && \
    # Drupal Console
    curl -sSL https://github.com/hechoendrupal/DrupalConsole/releases/download/$DRUPAL_CONSOLE_VERSION/drupal.phar -o /usr/local/bin/drupal && \
    chmod +x /usr/local/bin/drupal

# Add nginx service
RUN mkdir /etc/sv/apache2
ADD build/apache2/run.sh /etc/sv/apache2/run

# Add PHP service
RUN mkdir /etc/sv/phpfpm
ADD build/php/run.sh /etc/sv/phpfpm/run

# Add start script
RUN mkdir -p /etc/my_init.d
ADD start-container.sh /etc/my_init.d/start-container.sh

# Perms for services and Cron additions
RUN chmod +x /etc/my_init.d/*.sh && \
    chmod +x /etc/sv/*/run && \
    ln -s /etc/sv/apache2 /etc/service/ && \
    ln -s /etc/sv/phpfpm /etc/service/

RUN useradd -u 1001 -U --home /var/www/ -M -s /usr/sbin/nologin www-app

# Create web folders
RUN mkdir -p /var/www/html/ && \
    chown www-app:www-data -R /var/www/html/ && \
    chmod -R g+s /var/www/

VOLUME ["/var/www", "/var/logs/"]

# Workdir
WORKDIR /var/www

CMD ["/sbin/my_init"]

EXPOSE 22 80
