FROM ubuntu:latest
RUN apt-get clean && apt-get update
RUN apt-get install locales 

RUN locale-gen en_US.UTF-8 \
	&& export LANG=en_US.UTF-8 \
	&& apt-get update \
	&& apt-get install -y software-properties-common \
	&& apt-get install -y language-pack-en-base \
	&& LC_ALL=en_US.UTF-8 add-apt-repository -y ppa:ondrej/php \
	&& apt-get update \
    && apt-get -y install apache2 libapache2-mod-php5.6 php5.6 php5.6-cli php-xdebug php5.6-mbstring sqlite3 php5.6-mysql php-apcu php-apcu-bc php-imagick php-memcached php-pear curl imagemagick php5.6-dev php5.6-phpdbg php5.6-gd npm nodejs-legacy php5.6-json php5.6-curl php5.6-sqlite3 php5.6-intl apache2 vim git git-core wget libsasl2-dev libssl-dev libsslcommon2-dev libcurl4-openssl-dev autoconf g++ make openssl libssl-dev libcurl4-openssl-dev pkg-config libsasl2-dev libpcre3-dev \
	&& a2enmod headers \
	&& a2enmod rewrite \
	&& npm install -g grunt-cli bower \
	&& pecl channel-update pecl.php.net \
	&& pecl install mongodb \
	&& echo "extension=mongodb.so" >> /etc/php/5.6/apache2/php.ini \
	&& echo "extension=mongodb.so" >> /etc/php/5.6/cli/php.ini
RUN apt-get install -y php5.6-bcmath
RUN apt-get install php5.6-xml
RUN apt-get install -y php-soap && apt-get install -y php5.6-soap
COPY apache2.conf /etc/apache2/apache2.conf
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
RUN ln -sf /dev/stdout /var/log/apache2/access.log && \
    ln -sf /dev/stderr /var/log/apache2/error.log
RUN mkdir -p $APACHE_RUN_DIR $APACHE_LOCK_DIR $APACHE_LOG_DIR
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

VOLUME [ "/var/www/html" ]
WORKDIR /var/www/html

EXPOSE 80 443

ENTRYPOINT [ "/usr/sbin/apache2" ]
CMD ["-D", "FOREGROUND"]
