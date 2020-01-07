FROM alpine:latest
MAINTAINER Mark Olsson <post@markolsson.se>

RUN apk --update add wget \
	nginx \
	bash \
	supervisor \
	curl \
	git \
	php5-fpm \
	php5-pdo \
	php5-pdo_mysql \
	php5-mysql \
	php5-mysqli \
	php5-mcrypt \
	php5-xml \
	php5-ctype \
	php5-zlib \
	php5-curl \
	php5-openssl \
	php5-iconv \
	php5-json \
	php5-phar \
	php5-dom

# Uncomment if you want to build phalcon from source
#RUN apk --update add autoconf build-base php5-dev

RUN rm /var/cache/apk/* && \
	curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer && \
	mkdir -p /etc/nginx && \
	mkdir -p /run/nginx && \
	mkdir -p /var/log/supervisor && \
	rm /etc/nginx/nginx.conf

# Uncomment if you want to build phalcon from source
#RUN git clone --depth=1 git://github.com/phalcon/cphalcon.git /usr/local/src/cphalcon && cd /usr/local/src/cphalcon/build && ./install

ADD ./src/nginx.conf /etc/nginx/nginx.conf
ADD ./src/default /etc/nginx/sites-enabled/default
ADD ./src/supervisord.conf /etc/supervisord.conf
ADD ./src/start.sh /start.sh
ADD ./src/phalcon.so /usr/lib/php5/modules/phalcon.so
ADD ./src/phalcon.ini /etc/php5/conf.d/phalcon.ini

# tweak php-fpm config
RUN sed -i -e "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/g" /etc/php5/php.ini										   && \
	sed -i -e "s/upload_max_filesize\s*=\s*2M/upload_max_filesize = 500M/g" /etc/php5/php.ini						  && \
	sed -i -e "s/post_max_size\s*=\s*8M/post_max_size = 500M/g" /etc/php5/php.ini									  && \
	sed -i -e "s/variables_order = \"GPCS\"/variables_order = \"EGPCS\"/g" /etc/php5/php.ini						   && \
	sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php5/php-fpm.conf										 && \
	sed -i -e "s/error_log = \/var\/log\/php-fpm.log;/error_log = \/proc\/self\/fd\/2;/g" /etc/php5/php-fpm.conf	   && \
	sed -i -e "s/;catch_workers_output\s*=\s*yes/catch_workers_output = yes/g" /etc/php5/php-fpm.conf				  && \
	sed -i -e "s/pm.max_children = 5/pm.max_children = 9/g" /etc/php5/php-fpm.conf									 && \
	sed -i -e "s/pm.start_servers = 2/pm.start_servers = 3/g" /etc/php5/php-fpm.conf								   && \
	sed -i -e "s/pm.min_spare_servers = 1/pm.min_spare_servers = 2/g" /etc/php5/php-fpm.conf						   && \
	sed -i -e "s/pm.max_spare_servers = 3/pm.max_spare_servers = 4/g" /etc/php5/php-fpm.conf						   && \
	sed -i -e "s/;pm.max_requests = 500/pm.max_requests = 200/g" /etc/php5/php-fpm.conf								&& \
	sed -i -e "s/user = nobody/user = nginx/g" /etc/php5/php-fpm.conf												  && \
	sed -i -e "s/group = nobody/group = nginx/g" /etc/php5/php-fpm.conf												&& \
	sed -i -e "s/;listen.mode = 0660/listen.mode = 0666/g" /etc/php5/php-fpm.conf									  && \
	sed -i -e "s/;listen.owner = nobody/listen.owner = nginx/g" /etc/php5/php-fpm.conf								 && \
	sed -i -e "s/;listen.group = nobody/listen.group = nginx/g" /etc/php5/php-fpm.conf								 && \
	sed -i -e "s/listen = 127.0.0.1:9000/listen = \/var\/run\/php-fpm.sock/g" /etc/php5/php-fpm.conf				   && \
	rm -Rf /etc/nginx/conf.d/*				&& \
	rm -Rf /etc/nginx/sites-available/default && \
	mkdir -p /etc/nginx/ssl/				  && \
	chmod 755 /start.sh					   && \
	find /etc/php5/conf.d/ -name "*.ini" -exec sed -i -re 's/^(\s*)#(.*)/\1;\2/g' {} \;

# Expose Ports
EXPOSE 443 80

# Start Supervisord
CMD ["/bin/sh", "/start.sh"]
