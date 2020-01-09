FROM ubuntu:14.04
MAINTAINER Foo Bar <foo@bar.com>

ENV DEBIAN_FRONTEND noninteractive

RUN echo '#!/bin/sh\nexit 101' | sudo tee /usr/sbin/policy-rc.d > /dev/null
RUN sudo chmod +x /usr/sbin/policy-rc.d
RUN apt-get update
RUN apt-get install -y nginx
RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf
RUN chown -R www-data:www-data /var/lib/nginx

VOLUME ["/data", "/etc/nginx/site-enabled", "/var/log/nginx"]

WORKDIR /etc/nginx

CMD ["nginx"]

EXPOSE 80
EXPOSE 443
