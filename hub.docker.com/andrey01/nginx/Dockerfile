FROM centos:7
MAINTAINER Andrey Arapov <andrey.arapov@nixaid.com>

WORKDIR /root

RUN yum -y install epel-release && \
    yum -y update && \
    yum -y install make gcc pcre-devel zlib-devel \
                   inotify-tools \
                   glibc-static perl

# Compile runit
# Deps: glibc-static
ENV RUNIT_NAME "runit-2.1.2"
ENV RUNIT_HASH "6fd0160cb0cf1207de4e66754b6d39750cff14bb0aa66ab49490992c0c47ba18"

RUN pushd /opt && \
    curl -#L -o $RUNIT_NAME.tar.gz http://smarden.org/runit/$RUNIT_NAME.tar.gz && \
    sha256sum $RUNIT_NAME.tar.gz |grep -qw $RUNIT_HASH && \
    tar xf $RUNIT_NAME.tar.gz && \
    rm -f $RUNIT_NAME.tar.gz && \
    pushd admin/$RUNIT_NAME && \
    find . -xdev -type f -name "fmt_ptime.c" -exec sed -i.orig 's;gmtime;localtime;g' '{}' \; && \
    package/install && \
    package/install-man

# Compile socklog
#ENV SOCKLOG_NAME "socklog-2.1.0"
#ENV SOCKLOG_HASH "aa869a787ee004da4e5509b5a0031bcc17a4ab4ac650c2ce8d4e488123acb455"

#RUN pushd /opt && \
#    curl -#L -o $SOCKLOG_NAME.tar.gz http://smarden.org/socklog/$SOCKLOG_NAME.tar.gz && \
#    sha256sum $SOCKLOG_NAME.tar.gz |grep -qw $SOCKLOG_HASH && \
#    tar xf $SOCKLOG_NAME.tar.gz && \
#    rm -f $SOCKLOG_NAME.tar.gz && \
#    pushd admin/$SOCKLOG_NAME && \
#    package/install && \
#    package/install-man


# runit-docker - painlessly use Runit in Docker containers
RUN curl -#L -o runit-docker.tar.gz https://github.com/pixers/runit-docker/archive/master.tar.gz && \
    tar xf runit-docker.tar.gz && \
    cd runit-docker-master/ && \
    make && \
    make install && \
    sed -i 's;runsvdir;runsvdir -P;g' /sbin/runit-docker


# Global variables
ENV GPG_KEY_SERVER "pgp.mit.edu"


# Obtain the OpenSSL
# Deps: perl
ENV OPENSSL_NAME "openssl-1.0.2h"
ENV OPENSSL_GPGKEY_FP "8657ABB260F056B1E5190839D9C4D26D0E604491"

RUN curl -#L -o $OPENSSL_NAME.tar.gz https://www.openssl.org/source/$OPENSSL_NAME.tar.gz && \
    curl -#L -o $OPENSSL_NAME.tar.gz.asc https://www.openssl.org/source/$OPENSSL_NAME.tar.gz.asc && \
    gpg2 --keyserver $GPG_KEY_SERVER --recv-key $OPENSSL_GPGKEY_FP && \
    gpg2 -v $OPENSSL_NAME.tar.gz.asc && \
    tar xf $OPENSSL_NAME.tar.gz && \
    rm -f $OPENSSL_NAME.tar.gz


# Compile nginx
# Deps: make gcc pcre-devel zlib-devel
ENV NGINX_NAME "nginx-1.10.1"
ENV NGINX_GPGKEY_FP "B0F4253373F8F6F510D42178520A9993A1C052F8"

RUN curl -#L -o $NGINX_NAME.tar.gz https://nginx.org/download/$NGINX_NAME.tar.gz && \
    curl -#L -o $NGINX_NAME.tar.gz.asc https://nginx.org/download/$NGINX_NAME.tar.gz.asc && \
    gpg2 --keyserver $GPG_KEY_SERVER --recv-keys $NGINX_GPGKEY_FP && \
    gpg2 -v $NGINX_NAME.tar.gz.asc && \
    tar xf $NGINX_NAME.tar.gz && \
    rm -f $NGINX_NAME.tar.gz && \
    pushd $NGINX_NAME && \
    ./configure --prefix=/usr/share/nginx \
                --sbin-path=/usr/sbin/nginx \
                --conf-path=/etc/nginx/nginx.conf \
                --error-log-path=/var/log/nginx/error.log \
                --http-log-path=/var/log/nginx/access.log \
                --http-client-body-temp-path=/var/lib/nginx/tmp/client_body \
                --http-proxy-temp-path=/var/lib/nginx/tmp/proxy \
                --http-fastcgi-temp-path=/var/lib/nginx/tmp/fastcgi \
                --http-uwsgi-temp-path=/var/lib/nginx/tmp/uwsgi \
                --http-scgi-temp-path=/var/lib/nginx/tmp/scgi \
                --pid-path=/run/nginx.pid \
                --lock-path=/run/lock/subsys/nginx \
                --user=nginx \
                --group=nginx \
                --with-http_ssl_module \
                --with-openssl=../$OPENSSL_NAME \
                --with-openssl-opt="-fPIC" \
                --with-http_v2_module \
                --with-file-aio \
                --with-ipv6 \
                --with-ld-opt="-pie -Wl,-z,relro,-z,now -Wl,--as-needed" \
                --with-cc-opt="-O2 \
                               -fPIC \
                               -fstack-protector-all \
                               --param=ssp-buffer-size=4 \
                               -Wformat -Werror=format-security \
                               -Wp,-D_FORTIFY_SOURCE=2" && \
    make -j$(nproc) && \
    make install && \
    popd && \
    rm -rf $NGINX_NAME $OPENSSL_NAME


RUN useradd -u 1000 -d /var/lib/nginx -s /sbin/nologin nginx && \
    mkdir -m=0700 -p /etc/nginx/conf.d \
                     /var/lib/nginx/tmp/client_body \
                     /var/lib/nginx/tmp/fastcgi_temp \
                     /var/lib/nginx/tmp/proxy_temp \
                     /var/lib/nginx/tmp/scgi_temp \
                     /var/lib/nginx/tmp/uwsgi_temp && \
    chown -Rh nginx:root /var/lib/nginx


COPY nginx.conf /etc/nginx/nginx.conf
COPY service /etc/service/
RUN chmod +x -- /etc/service/*/run /etc/service/*/log/run

ENTRYPOINT ["/sbin/runit-docker"]
VOLUME ["/var/log/nginx"]
EXPOSE 80 443
