FROM        nginx
MAINTAINER  marven
EXPOSE      80 443
RUN         service nginx stop
RUN         rm /etc/nginx/conf.d/default.conf
COPY        conf/nginx/ /etc/nginx/
RUN         service nginx start