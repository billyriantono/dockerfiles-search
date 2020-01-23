FROM richarvey/nginx-php-fpm
MAINTAINER Dominik Fretz <dominik@openrov.com>

RUN sudo apt-get update && sudo apt-get install -y php5-redis

RUN mv /etc/php5/fpm/conf.d /etc/php5/fpm/conf.d_orig
RUN mkdir -p /etc/php5/fpm/conf.d && \
    mkdir -p /data/codebase

RUN groupadd -g 1000 nginx-data && \
 	useradd -g nginx-data -u 1000 -d /dev/zero -s /dev/false nginx-data
RUN chown -Rf nginx-data.nginx-data /data/codebase

RUN sed -i -e"s/user www-data/user nginx-data nginx-data/" /etc/nginx/nginx.conf #change the user to nginx-data which is the same UID as ubuntu on the underlying system to prevent issues with kohana logs and cache
# fix ownership of sock file for php-fpm as our version of nginx runs as nginx
RUN sed -i -e "s/^user = www-data/user = nginx-data/g" /etc/php5/fpm/pool.d/www.conf
RUN sed -i -e "s/^group = www-data/group = nginx-data/g" /etc/php5/fpm/pool.d/www.conf
RUN sed -i -e "s/^listen.owner = www-data/listen.owner = nginx-data/g" /etc/php5/fpm/pool.d/www.conf
RUN sed -i -e "s/^listen.group = www-data/listen.group = nginx-data/g" /etc/php5/fpm/pool.d/www.conf

# Add nginx config
ADD ./docker/nginx-default.conf /etc/nginx/sites-available/default.conf
ADD ./docker/nginx-http-only.conf /etc/nginx/sites-available/http-only.conf
RUN mkdir -p /data/codebase/application/cache /data/codebase/application/logs && \ 
    chown -R nginx-data /data/codebase/application/logs && \ 
    chown -R nginx-data /data/codebase/application/cache

# Start Supervisord
ADD ./docker/start-oe.sh /start-oe.sh
RUN chmod 755 /start-oe.sh

#Add code
ADD ./application /data/codebase/application
ADD ./modules /data/codebase/modules
ADD ./system /data/codebase/system
ADD ./www /data/codebase/www

VOLUME /data/codebase
VOLUME /data/codebase/application/logs

EXPOSE 80
EXPOSE 443

CMD ["/bin/bash", "/start-oe.sh"]
