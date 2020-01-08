FROM debian:stretch

MAINTAINER Laurent RICHARD "easylo@gmail.com"

ENV NGINX_VERSION 1.13.10

COPY nginx-json-log-module /nginx-json-log-module

RUN apt-get update && \
    apt-get -y install gettext curl build-essential libpcre3 libpcre3-dev zlib1g-dev libssl-dev git  libjansson-dev && \
    curl -LO http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz && \
    tar zxf nginx-${NGINX_VERSION}.tar.gz && \
    cd nginx-${NGINX_VERSION} && \
    git clone https://github.com/anomalizer/ngx_aws_auth.git && cd ngx_aws_auth && git checkout AuthV2&& cd .. && \
    ./configure --with-http_ssl_module --add-module=ngx_aws_auth --add-module=/nginx-json-log-module --prefix=/etc/nginx --conf-path=/var/log/nginx --conf-path=/etc/nginx/nginx.conf --sbin-path=/usr/sbin/nginx && \
    make install && \
    cd /tmp && \
    rm -f nginx-${NGINX_VERSION}.tar.gz && \
    rm -rf nginx-${NGINX_VERSION} && \
    apt-get purge -y curl git && \
    apt-get autoremove -y && \
    update-rc.d -f nginx remove && \
    rm -f /etc/nginx/sites-enabled/default && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


# forward request and error logs to docker log collector
# RUN ln -sf /dev/stdout /var/log/nginx/access.log \
# 	&& ln -sf /dev/stderr /var/log/nginx/error.log

COPY entrypoint.sh /sbin/entrypoint.sh
RUN chmod a+x /sbin/entrypoint.sh

COPY default.conf /default.conf
COPY nginx.conf /etc/nginx/nginx.conf

# Define mountable directories.
VOLUME ["/etc/nginx/sites-enabled", "/etc/nginx/certs", "/etc/nginx/conf.d", "/var/log/nginx", "/var/www/html"]

EXPOSE 80 443

ENTRYPOINT ["/sbin/entrypoint.sh"]
