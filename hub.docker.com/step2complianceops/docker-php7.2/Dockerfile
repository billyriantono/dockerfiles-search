FROM phusion/baseimage:0.11

# Regenerate SSH host keys.
# RUN /etc/my_init.d/00_regen_ssh_host_keys.sh

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]
ENV DEBIAN_FRONTEND=noninteractive

RUN echo "America/New_York" | tee /etc/timezone
RUN apt-add-repository -y ppa:nginx/stable
RUN apt-get update --fix-missing
RUN apt-get upgrade -y

#------------------------------
# Install Utilities
#------------------------------
RUN apt-get install -y \
	ant \
	build-essential \
	curl \
	default-jdk-headless \
	git \
	libbcprov-java \
	libcommons-lang3-java \
	poppler-utils \
	python-minimal \
	python-pip \
	software-properties-common \
	tzdata \
	vim \
	wget \
	zip

#------------------------------
# Install pdftk
#------------------------------
RUN git clone https://gitlab.com/pdftk-java/pdftk.git && cd /pdftk && git checkout tags/v3.0.3
RUN mkdir /pdftk/lib && ln -st /pdftk/lib /usr/share/java/commons-lang3.jar && ln -st /pdftk/lib /usr/share/java/bcprov.jar
RUN cd /pdftk && ant jar
ADD .deploy/devops/build/scripts/pdftk.sh /pdftk/build/jar
RUN cd /pdftk/build/jar && cat pdftk.sh pdftk.jar > /usr/local/bin/pdftk
RUN chmod +x /usr/local/bin/pdftk

#------------------------------
# Install and configure PHP-FPM
#------------------------------
RUN apt-get install -y --no-install-recommends \
	php7.2-bcmath \
	php7.2-cli \
    php7.2-curl \
    php7.2-dev \
	php7.2-fpm \
    php7.2-gd \
    php7.2-gmp \
    php7.2-intl \
    php7.2-json \
    php7.2-mbstring \
    php7.2-mysql \
    php7.2-opcache \
    php7.2-pgsql \
    php7.2-readline \
    php7.2-xml \
    php7.2-xsl \
    php7.2-zip \
    php-memcached \
	php-pear \
    php-redis

# build the daemon
RUN mkdir /etc/service/phpfpm
ADD .deploy/devops/build/daemons/phpfpm.sh /etc/service/phpfpm/run
RUN chmod +x /etc/service/phpfpm/run

# Install composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/bin/composer
RUN echo "/root/ec2/.composer" > /etc/container_environment/COMPOSER_HOME

#------------------------------
# Install PECL dependencies
#------------------------------
#RUN pecl install stats
RUN pecl channel-update pecl.php.net
RUN pecl install https://pecl.php.net/get/stats-2.0.3.tgz

ADD .deploy/devops/resource/php/stats.ini /etc/php/7.2/mods-available
RUN ln -sf /etc/php/7.2/mods-available/stats.ini /etc/php/7.2/cli/conf.d/20-stats.ini
RUN ln -sf /etc/php/7.2/mods-available/stats.ini /etc/php/7.2/fpm/conf.d/20-stats.ini

#-------------------------------
# Install NewRelic PHP Agent
#-------------------------------
RUN wget -O - https://download.newrelic.com/548C16BF.gpg | apt-key add -
RUN sh -c 'echo "deb http://apt.newrelic.com/debian/ newrelic non-free" > /etc/apt/sources.list.d/newrelic.list'
RUN apt-get update
RUN apt-get install -y newrelic-php5

#------------------------------
# Install PIP dependencies
#------------------------------
RUN pip install boto3==1.3.0

#------------------------------
# Install and configure Nginx
#------------------------------
RUN apt-get install -y nginx

# Create default app directory
RUN rm -rf /var/www
ADD . /var/www

ADD .deploy/devops/build/default /etc/nginx/sites-available/default
ADD .deploy/devops/build/http_realip.conf /etc/nginx/conf.d/http_realip.conf

# Shell script must run the daemon without letting it daemonize/fork it
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

# build the daemon
RUN mkdir /etc/service/nginx
ADD .deploy/devops/build/daemons/nginx.sh /etc/service/nginx/run
RUN chmod +x /etc/service/nginx/run

#------------------------------
# Install and configure Queue
#------------------------------
RUN mkdir /etc/service/queue
ADD .deploy/devops/build/daemons/queue.sh /etc/service/queue/run
RUN chmod +x /etc/service/queue/run

#------------------------------
# Startup Scripts
#------------------------------

# create script directory
RUN mkdir -p /etc/my_init.d

# add scripts
ADD .deploy/devops/build/scripts/envars.sh /etc/my_init.d/01_envars.sh
ADD .deploy/devops/build/scripts/composer.sh /etc/my_init.d/02_composer.sh
ADD .deploy/devops/build/scripts/permissions.sh /etc/my_init.d/03_permissions.sh
ADD .deploy/devops/build/scripts/php-fpm.sh /etc/my_init.d/04_php-fpm.sh
ADD .deploy/devops/build/scripts/newrelic.sh /etc/my_init.d/05_newrelic.sh
ADD .deploy/devops/build/scripts/cron.sh /etc/my_init.d/06_cron.sh
ADD .deploy/devops/build/scripts/dot_env.sh /etc/my_init.d/07_dot_env.sh

# update script permissions
RUN chmod +x /etc/my_init.d/*

#------------------------------
# Finish and Cleanup
#------------------------------

EXPOSE 80

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*