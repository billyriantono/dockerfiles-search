FROM centos:7
MAINTAINER Rajeev Kulshrestha rajeev.kulshrestha@ocio.usda.gov
ENV PATH /usr/local/src/vendor/bin/:/usr/local/rvm/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# Set TERM env to avoid mysql client error message "TERM environment variable not set" when running from inside the container
ENV TERM xterm

# Fix command line compile issue with bundler.
ENV LC_ALL en_US.utf8

# Custom docroot (see conf/run-httpd.sh)

ENV DOCROOT /var/www/public

ENV DRUPAL_VERSION 7.56

# Install and enable repositories
RUN yum -y update && \
    yum -y install epel-release && \
    rpm -Uvh https://centos7.iuscommunity.org/ius-release.rpm && \
    yum -y update

RUN yum -y install \
    curl \
    git2u \
    mariadb \
    MariaDB-server \
    MariaDB-client  \
    msmtp \
    net-tools \
    python34 \
    vim \
    wget \
    rsync 
        
# Install PHP and PHP modules
RUN yum -y install \
    php70u \
    php70u-curl \
    php70u-gd \
    php70u-imap \
    php70u-mbstring \
    php70u-mcrypt \
    php70u-mysql \
    php70u-odbc \
    php70u-pear \
    php70u-mysqlnd \
    php70u-pecl-imagick \
    php70u-pecl-json \
    php70u-pecl-zendopcache \
    php70u-redis \
    php70u-pecl-redis
    
# Install misc tools
RUN yum -y install \
    python-setuptools

# Perform yum cleanup
RUN yum -y upgrade && \
    yum clean all

# Install Composer and Drush
RUN curl -sS https://getcomposer.org/installer | php -- \
    --install-dir=/usr/local/bin \
    --filename=composer \
    --version=1.2.0 && \
    composer \
    --working-dir=/usr/local/src/ \
    global \
    require \
    drush/drush:8.* && \
    ln -s /usr/local/src/vendor/bin/drush /usr/bin/drush

RUN drush dl registry_rebuild-7.x


# Install Drupal Console. Set to minimum 
# stability to dev.
RUN curl https://drupalconsole.com/installer -L -o drupal.phar && \
	mv drupal.phar /usr/local/bin/drupal && \
	chmod +x /usr/local/bin/drupal
RUN drupal init

# Install Drupal.
RUN rm -rf /var/www/public
RUN cd /var && \
	drush dl drupal-$DRUPAL_VERSION && \
	mv /var/drupal* /var/www/public
RUN mkdir -p /var/www/public/sites/default/files && \
	chmod a+w /var/www/public/sites/default -R && \
	mkdir /var/www/public/sites/all/modules/contrib -p && \
	mkdir /var/www/public/sites/all/modules/custom && \
	mkdir /var/www/public/sites/all/themes/contrib -p && \
	mkdir /var/www/public/sites/all/themes/custom && \
	cp /var/www/public/sites/default/default.settings.php /var/www/public/sites/default/settings.php && \
	chmod 0664 /var/www/public/sites/default/settings.php && \
	chown -R root:root /var/www/public
RUN cd /var/www/public && \
	drush si -y standard --db-url=mysql://root:@localhost/drupal --account-pass=admin && \
	drush dl admin_menu devel && \
	# In order to enable Simpletest, we need to download PHPUnit.
	composer install --dev && \
	# Admin Menu is broken. See https://www.drupal.org/node/2563867 for more info.
	# As long as it is not fixed, only enable simpletest and devel.
	# drush en -y admin_menu simpletest devel
	drush en -y simpletest devel && \
	drush en -y bartik
RUN /etc/init.d/mysql start && \
	cd /var/www/public && \
	drush cset system.theme default 'bartik' -y
    
# Allow Kernel and Browser tests to be run via PHPUnit.	
RUN sed -i 's/name="SIMPLETEST_DB" value=""/name="SIMPLETEST_DB" value="sqlite:\/\/localhost\/tmp\/db.sqlite"/' /var/www/public/core/phpunit.xml.dist

# Apache config, and PHP config, test apache config
# See https://github.com/docker/docker/issues/7511 /tmp usage
COPY public/index.php /var/www/public/index.php
COPY centos-7 /tmp/centos-7/

RUN rsync -a /tmp/centos-7/etc/ /etc/ && \
    apachectl configtest

EXPOSE 80 443

# Simple startup script to avoid some issues observed with container restart 
ADD conf/run-httpd.sh /run-httpd.sh
RUN chmod -v +x /run-httpd.sh

ADD conf/mail.ini /etc/php.d/mail.ini
RUN chmod 644 /etc/php.d/mail.ini

CMD ["/run-httpd.sh"]