FROM phusion/baseimage:0.10.1

MAINTAINER Pavels Fjodorovs (pavels.fjodorovs@hotelplan.com)

ENV BUILD 10.08.2018

ENV HOME /root

ENV TIMEZONE Europe/Berlin
ENV APP_ROOT app

RUN /etc/my_init.d/00_regen_ssh_host_keys.sh

CMD ["/sbin/my_init"]

# Nginx-PHP Installation
RUN touch /etc/apt/apt.conf.d/99fixbadproxy \
  && echo "Acquire::http::Pipeline-Depth 0;" >> /etc/apt/apt.conf.d/99fixbadproxy \
  && echo "Acquire::http::No-Cache true;" >> /etc/apt/apt.conf.d/99fixbadproxy \
  && echo "Acquire::BrokenProxy true;" >> /etc/apt/apt.conf.d/99fixbadproxy \
  && add-apt-repository -y ppa:ondrej/php \
  && add-apt-repository -y ppa:nginx/stable \
  && add-apt-repository -y ppa:stesie/libv8 \
  && apt-get update -o Acquire::CompressionTypes::Order::=gz \
  && apt-get install -y --force-yes --fix-missing git vim curl wget ssl-cert libcurl4-gnutls-dev php7.1-cli php7.1-fpm php7.1-mysql\
               php7.1-gd php7.1-mcrypt php7.1-intl php7.1-pgsql php7.1-sqlite php7.1-curl\
               php7.1-imap php7.1-tidy php-pear php7.1-dev php7.1-xsl php7.1-mbstring\
               libxml2-dev unzip libz-dev libicu-dev nano libmagickwand-dev imagemagick\
               php7.1-soap php7.1-opcache nginx \
               libv8-7.5 libv8-7.5-dev \
			   libhiredis-dev \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# http://askubuntu.com/questions/76808/how-to-use-variables-in-sed-command
# Setup timezone
RUN sed -i "s|;date.timezone =.*|date.timezone = $TIMEZONE|" /etc/php/7.1/fpm/php.ini \
    && sed -i "s|;date.timezone =.*|date.timezone = $TIMEZONE|" /etc/php/7.1/cli/php.ini

# Install Composer:
RUN curl -s https://getcomposer.org/installer | php \
  && mv composer.phar /usr/local/bin/composer \
  && chmod +x /usr/local/bin/composer
ENV COMPOSER_HOME /var/www

RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php/7.1/fpm/php-fpm.conf \
  && sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/" /etc/php/7.1/fpm/php.ini

# Add github and bitbucket keys to known hosts
RUN ssh-keyscan -t rsa github.com 2>&1 >> /root/.ssh/known_hosts \
 && ssh-keyscan -t rsa bitbucket.org 2>&1 >> /root/.ssh/known_hosts

# Install imagick PHP Extension
RUN pecl channel-update pecl.php.net \
  && pecl install imagick \
  && echo extension=imagick.so > /etc/php/7.1/mods-available/imagick.ini \
  && ln -s /etc/php/7.1/mods-available/imagick.ini /etc/php/7.1/fpm/conf.d/20-imagick.ini \
  && ln -s /etc/php/7.1/mods-available/imagick.ini /etc/php/7.1/cli/conf.d/20-imagick.ini

# xdebug
RUN pecl install xdebug \
  && echo "zend_extension=/usr/lib/php/20160303/xdebug.so" > /etc/php/7.1/mods-available/xdebug.ini \
  && sed -i '1 a xdebug.remote_mode=req' /etc/php/7.1/mods-available/xdebug.ini \
  && sed -i '1 a xdebug.remote_handler=dbgp' /etc/php/7.1/mods-available/xdebug.ini \
  && sed -i '1 a xdebug.max_nesting_level=1200' /etc/php/7.1/mods-available/xdebug.ini \
  && sed -i '1 a xdebug.remote_port=9000' /etc/php/7.1/mods-available/xdebug.ini \
  && sed -i '1 a xdebug.remote_enable=1' /etc/php/7.1/mods-available/xdebug.ini \
  && sed -i '1 a xdebug.remote_host=host.docker.internal' /etc/php/7.1/mods-available/xdebug.ini \
  && sed -i '1 a xdebug.profiler_enable_trigger=1' /etc/php/7.1/mods-available/xdebug.ini \
  && sed -i '1 a xdebug.profiler_output_dir=/app/var' /etc/php/7.1/mods-available/xdebug.ini \
  && ln -s /etc/php/7.1/mods-available/xdebug.ini /etc/php/7.1/fpm/conf.d/20-xdebug.ini
  # && ln -s /etc/php/7.1/mods-available/xdebug.ini /etc/php/7.1/cli/conf.d/20-xdebug.ini

# igbinary
RUN pecl install igbinary \
  && echo extension=igbinary.so > /etc/php/7.1/mods-available/igbinary.ini \
  && ln -s /etc/php/7.1/mods-available/igbinary.ini /etc/php/7.1/fpm/conf.d/50-igbinary.ini \
  && ln -s /etc/php/7.1/mods-available/igbinary.ini /etc/php/7.1/cli/conf.d/50-igbinary.ini

# phpiredis
RUN git clone https://github.com/Danack/phpiredis.git  \
    && cd phpiredis \
    && phpize && ./configure --enable-phpiredis \
    && make \
    && make install \
	&& echo "extension=phpiredis.so" > /etc/php/7.1/mods-available/phpiredis.ini \
	&& ln -s /etc/php/7.1/mods-available/phpiredis.ini /etc/php/7.1/fpm/conf.d/60-phpiredis.ini \
    && ln -s /etc/php/7.1/mods-available/phpiredis.ini /etc/php/7.1/cli/conf.d/60-phpiredis.ini

# Setup PHP
RUN sed -i "s|upload_max_filesize =.*|upload_max_filesize = 100M|" /etc/php/7.1/fpm/php.ini \
  && sed -i "s|post_max_size =.*|post_max_size = 101M|" /etc/php/7.1/cli/php.ini \
  && sed -i "s|memory_limit =.*|memory_limit = 3000M|" /etc/php/7.1/fpm/php.ini \
  && sed -i "s|memory_limit =.*|memory_limit = 3000M|" /etc/php/7.1/cli/php.ini \
  && sed -i "s|max_execution_time =.*|max_execution_time = 0|" /etc/php/7.1/fpm/php.ini  \
  && sed -i "s|max_execution_time =.*|max_execution_time = 0|" /etc/php/7.1/cli/php.ini

# Setup Timezone
RUN echo $TIMEZONE | tee /etc/timezone \
  && dpkg-reconfigure -f noninteractive tzdata

ENV RELATIVE_APP_ROOT web
ENV PHP_INDEX_FILE app.php
ENV V8_MODULE_VERSION 2.1.1

# V8
RUN cd /tmp \
  && git clone https://github.com/phpv8/v8js.git \
  && cd v8js \
  && git checkout tags/$V8_MODULE_VERSION \
  && phpize \
  && ./configure --with-v8js=/opt/libv8-7.5 \
  && make \
  && make test \
  && make install \
  && echo extension=v8js.so > /etc/php/7.1/mods-available/v8js.ini \
  && ln -s /etc/php/7.1/mods-available/v8js.ini /etc/php/7.1/fpm/conf.d/99-v8js.ini \
  && ln -s /etc/php/7.1/mods-available/v8js.ini /etc/php/7.1/cli/conf.d/99-v8js.ini \
  && rm -rf /tmp/*

# Setup nginx

# Prepare setup files
RUN mkdir -p /etc/my_init.d
ADD setup/nginx/setup.sh /etc/my_init.d/setup.sh
RUN chmod +x /etc/my_init.d/setup.sh

ADD setup/nginx/default   /etc/nginx/sites-available/default
RUN mkdir           /etc/service/nginx
ADD setup/nginx/nginx.sh  /etc/service/nginx/run
RUN chmod +x        /etc/service/nginx/run
RUN mkdir           /etc/service/phpfpm
ADD setup/nginx/phpfpm.sh /etc/service/phpfpm/run
RUN chmod +x        /etc/service/phpfpm/run
RUN mkdir /run/php/

VOLUME /uploads
VOLUME /var
ENV HOME /var/www

RUN usermod -s /bin/bash www-data \
  && usermod -d /var/www/ www-data

WORKDIR $APP_ROOT
