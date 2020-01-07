FROM ubuntu:trusty
MAINTAINER Alexander Johnson <alex@cldfzn.com>

ENV NGINX_VERSION 1.7.9-1+trusty2

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C300EE8C && \
    echo "deb http://ppa.launchpad.net/nginx/development/ubuntu trusty main" | tee -a /etc/apt/sources.list.d/nginx.list && \
    apt-get -qq update && \
    apt-get -qqy install nginx=${NGINX_VERSION} && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

VOLUME ["/var/cache/nginx"]
EXPOSE 80 443
CMD ["nginx", "-g", "daemon off;"]

