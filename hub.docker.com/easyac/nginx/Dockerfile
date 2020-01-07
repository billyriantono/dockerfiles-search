FROM nginx

MAINTAINER Ícaro Heimig

RUN apt-get -y update && \
    apt-get -y install git && \
    mkdir -p /ssl/easyac.xyz && \
    mkdir -p /ssl/api.easyac.xyz && \
    mkdir -p /ssl/docs.easyac.xyz && \
    mkdir -p /archive

RUN git clone https://github.com/easyac/apidocs /var/www/html

COPY nginx.conf /etc/nginx/nginx.conf
