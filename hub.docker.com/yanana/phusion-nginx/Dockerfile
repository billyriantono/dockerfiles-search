FROM phusion/baseimage

MAINTAINER Shun Yanaura <metroplexity@gmail.com>

ENV NGINX_VERSION 1.7.10-1~trusty

RUN curl -sS http://nginx.org/keys/nginx_signing.key | sudo apt-key add - && \
    echo 'deb http://nginx.org/packages/mainline/ubuntu/ trusty nginx' >> /etc/apt/sources.list && \
    echo 'deb-src http://nginx.org/packages/mainline/ubuntu/ trusty nginx' >> /etc/apt/sources.list && \
    apt-get update && apt-get install -y ca-certificates nginx=${NGINX_VERSION} && \
    rm -rf /var/lib/apt/lists/* && \
    ln -sf /dev/stdout /var/log/nginx/access.log && \
    ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
