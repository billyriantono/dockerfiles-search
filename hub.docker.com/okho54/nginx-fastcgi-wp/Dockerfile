FROM ubuntu:bionic

LABEL maintainer="Artem Bokhan <abokhan@setronica.net>"
LABEL description="Nginx http/https fastcgi-wp container"

VOLUME /var/www /etc/nginx/external /var/log/nginx

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections && \
    apt-get update && apt-get install -y curl gnupg && \
    cd /tmp && curl -sO https://nginx.org/keys/nginx_signing.key && \
    apt-key add nginx_signing.key && \
    echo "deb http://nginx.org/packages/ubuntu/ bionic nginx" >> /etc/apt/sources.list.d/nginx.list && \
    apt-get update && \
    apt-get install -y nginx && \
    apt-get clean

COPY files /

ENTRYPOINT ["/entrypoint.sh"]

CMD ["nginx"]
