FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update \	
	&& apt-get install -y software-properties-common \	
	&& add-apt-repository -y ppa:ondrej/php \
	&& apt-get install -y apache2 \
	&& apt-get install -y libapache2-mod-php7.2 \
	&& apt-get install -y php7.2 \
	&& apt-get install -y php7.2-cli \
	&& apt-get install -y php7.2-mysql \
		&& apt-get install -y php-xdebug php7.2-mbstring sqlite3 php-imagick php-memcached php-pear imagemagick php7.2-dev php7.2-phpdbg php7.2-gd php7.2-json php7.2-curl php7.2-soap php7.2-sqlite3 php7.2-intl php7.2-ldap php7.2-zip php-zip php-common php7.2-xml php-tokenizer\
	&& a2enmod headers \
	&& a2enmod rewrite \
	&& apt-get install -y curl \
	&& apt-get install -y vim \
	&& apt-get install -y wget \
	&& apt-get install -y make \
	&& apt-get install -y g++ \
	&& apt-get install -y git-core \
		&& apt-get install -y libsasl2-dev libssl-dev libcurl4-openssl-dev autoconf openssl libssl-dev libcurl4-openssl-dev pkg-config libsasl2-dev libpcre3-dev \
	&& apt-get install -y php7.2-bcmath \
	&& apt-get install -y unzip \
	&& apt-get install -y phpmd \
	&& apt-get install -y poppler-utils
	
RUN phpmd --version

# instala o composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
RUN ln -sf /dev/stdout /var/log/apache2/access.log && \
    ln -sf /dev/stderr /var/log/apache2/error.log
RUN mkdir -p $APACHE_RUN_DIR $APACHE_LOCK_DIR $APACHE_LOG_DIR

RUN sed -i -e 's/short_open_tag = Off/short_open_tag = On/g' /etc/php/7.2/cli/php.ini 

VOLUME [ "/var/www/html" ]
WORKDIR /var/www/html

EXPOSE 80

ENTRYPOINT [ "/usr/sbin/apache2" ]
CMD ["-D", "FOREGROUND"]