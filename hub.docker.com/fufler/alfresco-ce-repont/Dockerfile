FROM ubuntu:16.04
MAINTAINER Fred Liang <info@fredliang.cn>

# Keep upstart from complaining
RUN dpkg-divert --local --rename --add /sbin/initctl &&\
    ln -sf /bin/true /sbin/initctl

# Let the conatiner know that there is no tty
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
    apt-get -y upgrade && \
	apt-get install php7.0-fpm php7.0-mysql php7.0-gd php7.0-cli nginx curl git wget net-tools vim -y

# nginx config
# Reduce keepalive timeout to 2 seconds
RUN sed -i -e"s/keepalive_timeout\s*65/keepalive_timeout 2/" /etc/nginx/nginx.conf && \
	sed -i -e"s/keepalive_timeout 2/keepalive_timeout 2;\n\tclient_max_body_size 100m/" /etc/nginx/nginx.conf && \
	echo "daemon off;" >> /etc/nginx/nginx.conf

# php-fpm config
RUN sed -i -e "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/g" /etc/php/7.0/fpm/php.ini && \
	sed -i -e "s/upload_max_filesize\s*=\s*2M/upload_max_filesize = 100M/g" /etc/php/7.0/fpm/php.ini && \
	sed -i -e "s/post_max_size\s*=\s*8M/post_max_size = 100M/g" /etc/php/7.0/fpm/php.ini && \
	sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php/7.0/fpm/php-fpm.conf && \
	sed -i -e "s|/run/php/php7.0-fpm.pid|/var/run/php/php7.0-fpm.pid|g" /etc/php/7.0/fpm/php-fpm.conf && \
	sed -i -e "s|/run/php/php7.0-fpm.sock|/var/run/php/php7.0-fpm.sock|g" /etc/php/7.0/fpm/pool.d/www.conf && \
	sed -i -e "s/;catch_workers_output\s*=\s*yes/catch_workers_output = yes/g" /etc/php/7.0/fpm/pool.d/www.conf && \
	find /etc/php/7.0/fpm/conf.d/ -name "*.ini" -exec sed -i -re 's/^(\s*)#(.*)/\1;\2/g' {} \; && \
	mkdir -p /var/run/php && \
	mkdir -p /var/log/php-fpm

# nginx site conf
ADD ./site.conf /etc/nginx/sites-available/default

RUN apt-get install python-pip -y
# Supervisor Config
RUN /usr/bin/pip install supervisor supervisor-stdout
ADD ./supervisord.conf /etc/supervisord.conf

# ssl certs
# ADD  https://storage.fredliang.cn/certs.tar.gz /etc/nginx/certs.tar.gz

# Install Wordpress
ADD https://storage.fredliang.cn/space.tar.gz /var/www/space.tar.gz
RUN cd /var/www/ && rm -r html && tar xvzf space.tar.gz && rm /var/www/space.tar.gz && chown -R www-data:www-data /var/www/html 
# config ssl certs
#RUN cd /etc/nginx && tar xvzf certs.tar.gz && rm /etc/nginx/certs.tar.gz 

# Wordpress Initialization and Startup Script
ADD ./start.sh /start.sh
RUN chmod 755 /start.sh

# private expose
EXPOSE 80
EXPOSE 443
# volume for wordpress install
VOLUME ["/var/www/html"]

CMD ["/bin/bash", "/start.sh"]
