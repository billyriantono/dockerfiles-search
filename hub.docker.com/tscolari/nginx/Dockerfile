# RUBY MACHINE
FROM tscolari/base
MAINTAINER Tiago Scolari <tscolari@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN add-apt-repository ppa:nginx/stable && \
    apt-get update && \
    apt-get install nginx -y --force-yes && \
    apt-get clean -y && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

VOLUME /etc/nginx/
VOLUME /var/log/nginx

EXPOSE 80
EXPOSE 443
CMD nginx
