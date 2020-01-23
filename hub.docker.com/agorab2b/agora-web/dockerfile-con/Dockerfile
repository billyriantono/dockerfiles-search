FROM ubuntu:18.04 as build
LABEL maintainer="don@agilicus.com"

# This scary-looking variable only causes apt-key to not warn on the
# output not being stdout (output should not be parsed).
ENV APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=DontWarn

WORKDIR /src

RUN apt-get update && \
    apt-get install -y build-essential git tree wget software-properties-common && \
    add-apt-repository -y ppa:nginx/stable && \
    sed -i -e 's?^# ??' /etc/apt/sources.list.d/nginx-ubuntu-stable-bionic.list && \
    sed -i -e 's?# deb-src?deb-src?' /etc/apt/sources.list && \
    apt-get update && \
    apt-get -y build-dep nginx && \
    apt-get -y source nginx && \
    git clone https://github.com/AirisX/nginx_cookie_flag_module && \
    tar xvf nginx_1.16.1.orig.tar.gz && \
    mkdir -p modules && \
    cd nginx-1.16.1 && \
    ./configure --with-compat --add-dynamic-module=../nginx_cookie_flag_module/ && \
    make modules && \
    cp objs/ngx_http_cookie_flag_filter_module.so /src/modules

RUN cd /src && \
    wget -qO - https://openresty.org/package/pubkey.gpg | apt-key add - && \
    add-apt-repository -y "deb http://openresty.org/package/ubuntu $(lsb_release -sc) main" && \
    apt-get update && \
    apt-get -y source pcre3 && \
    apt-get -y install liblua5.1-dev python luarocks openresty && \
    git clone https://github.com/p0pr0ck5/lua-resty-waf && \
    cd lua-resty-waf && \
    git submodule init && \
    git submodule update && \
    (cd src; make PREFIX=/usr CFLAGS="-c -O3 -Wall -fpic"  decode.o) && \
    make PREFIX=/usr && \
    make PREFIX=/usr install
 
FROM ubuntu:18.04
RUN \
    apt-get update && \
    apt-get install -y wget gnupg2 && \
    wget -qO - https://openresty.org/package/pubkey.gpg | apt-key add - && \
    echo deb http://openresty.org/package/ubuntu bionic main | tee -a /etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y software-properties-common openresty luarocks liblua5.1-dev && \
    add-apt-repository -y ppa:nginx/stable && \
    apt-get update && \
    apt-get -y install nginx-extras && \
    dpkg -r build-essential && \
    apt-get -y autoremove

COPY --from=build /src/modules/* /usr/lib/nginx/modules/
COPY --from=build /usr/local/lib/lua /usr/local/lib/lua
COPY --from=build /usr/local/lib/luarocks /usr/local/lib/luarocks
