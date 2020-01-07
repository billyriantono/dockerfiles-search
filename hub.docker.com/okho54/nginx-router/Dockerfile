FROM ubuntu:bionic

LABEL maintainer="Artem Bokhan <abokhan@setronica.net>"
LABEL description="Nginx http/https router container"

EXPOSE 80/tcp 443/tcp
VOLUME /etc/nginx/external

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections && \
    apt-get update && apt-get install -y curl gnupg && \
    cd /tmp && curl -sO https://nginx.org/keys/nginx_signing.key && \
    apt-key add nginx_signing.key && \
    echo "deb http://nginx.org/packages/ubuntu/ bionic nginx" >> /etc/apt/sources.list.d/nginx.list && \
    apt-get update && \
    apt-get install -y nginx && \
    apt-get clean

COPY files /

CMD ["nginx"]
