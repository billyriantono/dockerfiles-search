# Nginx and PHP5 bas
# http://wiki.nginx.org/
# http://us.php.net/

FROM ubuntu:trusty
MAINTAINER Jean-Marc Lagace <jean-marc@m2i3.com>

# Set noninteractive mode for apt-get
ENV LANG=en_US.UTF-8 LC_ALL=en_US.UTF-8 DEBIAN_FRONTEND=noninteractive

# make sure we have the latest and greatest
RUN		locale-gen en_US.UTF-8 \
	&&	apt-get update \
	&&	apt-get install -y \
		software-properties-common \
		python-software-properties \
		curl \
		nginx \
		supervisor \
		mysql-client \
		php5-fpm \
		php5-mysql \
		php-apc php5-imagick php5-imap php5-mcrypt php5-gd libssh2-php \
		php5-curl php5-gd php5-intl php-pear php5-imagick php5-imap php5-mcrypt \
		php5-memcache php5-ming php5-ps php5-pspell php5-recode php5-sqlite php5-tidy php5-xmlrpc php5-xsl \
		libssl-dev \
		php5-dev build-essential \
		nullmailer \
	&&	rm -rf /var/lib/apt/lists/*

#RUN pecl install zendopcache-7.0.3
#    php5-dev \ 
#RUN pecl install zendopcache-beta

#RUN apt-get remove -y php5-dev build-essential && \
#    apt-get autoremove -y && apt-get autoclean -y

COPY nginx.conf /etc/nginx/nginx.conf
ADD https://raw.github.com/h5bp/server-configs-nginx/master/h5bp/location/expires.conf /etc/nginx/conf/expires.conf 
ADD https://raw.github.com/h5bp/server-configs-nginx/master/h5bp/location/expires.conf /etc/nginx/conf/expires.conf 
ADD https://raw.github.com/h5bp/server-configs-nginx/master/h5bp/directive-only/x-ua-compatible.conf /etc/nginx/conf/x-ua-compatible.conf 
ADD https://raw.github.com/h5bp/server-configs-nginx/master/h5bp/location/cross-domain-fonts.conf /etc/nginx/conf/cross-domain-fonts.conf 
ADD https://raw.github.com/h5bp/server-configs-nginx/master/h5bp/directive-only/cross-domain-insecure.conf /etc/nginx/h5bp/directive-only/cross-domain-insecure.conf 
ADD https://raw.github.com/h5bp/server-configs-nginx/master/h5bp/location/protect-system-files.conf /etc/nginx/conf/protect-system-files.conf

COPY nginx-site.conf /etc/nginx/sites-available/default

COPY opcache.ini /etc/php5/conf.d/20-opcache.ini
RUN		echo "cgi.fix_pathinfo = 0;" >> /etc/php5/fpm/php.ini \
	&&	sed -i -e '/access_log/d' /etc/nginx/conf/expires.conf \
	&&	sed -i -e 's/^listen =.*/listen = 127.0.0.1:7777/' /etc/php5/fpm/pool.d/www.conf \
	&&	sed -i -e 's/^short_open_tag =.*/short_open_tag = On/' /etc/php5/fpm/php.ini \
# FIX FOR MCRYPT not being enabled
	&&	php5enmod mcrypt

# supervisor
ADD supervisor/  /etc/supervisor/conf.d/

# Decouple our data from our container.
#VOLUME /data
VOLUME /var/log/nginx

EXPOSE 80
ADD startup/ /usr/lib/startup.d/
ADD start.sh /start.sh
RUN chmod +x /usr/lib/startup.d/* && chmod +x /start.sh
CMD [ "/start.sh" ]