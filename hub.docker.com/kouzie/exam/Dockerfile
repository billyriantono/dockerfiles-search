FROM ubuntu:14.04
MAINTAINER "kouzie"

RUN apt-get update && apt-get install -y nginx
RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf
RUN chown -R www-data:www-data /var/lib/nginx
VOLUME [ "/data", "/etc/niginx/site-enabled", "/var/log/nginx" ]
WORKDIR /etc/nginx
CMD [ "nginx" ]
EXPOSE 80
EXPOSE 443