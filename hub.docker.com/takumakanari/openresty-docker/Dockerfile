FROM centos:latest
MAINTAINER Takuma kanari <chemtrails.t@gmail.com>

RUN yum update -y && \
    yum install -y perl pcre pcre-devel zlib zlib-devel openssl openssl-devel wget tar gcc-c++ && \
    yum clean all

RUN rm -rf ngx_openresty-1.7.10.2 && \
    wget -O - https://openresty.org/download/ngx_openresty-1.7.10.2.tar.gz | tar zxf - && \
    cd ngx_openresty-1.7.10.2 && \
    ./configure \
     --user=nginx \
     --group=nginx \
     --prefix=/usr/share/nginx \
     --sbin-path=/usr/sbin/nginx \
     --conf-path=/etc/nginx/nginx.conf \
     --error-log-path=/dev/stderr \
     --http-log-path=/dev/stdout \
     --http-client-body-temp-path=/var/lib/nginx/tmp/client_body \
     --http-proxy-temp-path=/var/lib/nginx/tmp/proxy && \
    gmake && \
    gmake install && \
    cd ../ && \
    rm -rf ngx_openresty-1.7.10.2 && \
    mkdir -p /var/lib/nginx/tmp/uwsgi /var/lib/nginx/tmp/client_body && \
    useradd nginx --no-create-home && \
    chown -R nginx:nginx /var/lib/nginx/tmp/uwsgi /var/lib/nginx/tmp/client_body && \
    rm -rf /etc/nginx/*

COPY files/etc /etc
VOLUME ["/etc/nginx/conf.d"]

CMD ["/usr/sbin/nginx", "-c", "/etc/nginx/nginx.conf"]
