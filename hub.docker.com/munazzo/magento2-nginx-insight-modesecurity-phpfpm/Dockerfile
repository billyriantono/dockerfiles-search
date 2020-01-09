FROM php:7.2.11-fpm

MAINTAINER A. Gökay Duman <aligokayduman@gmail.com>

ENV NPS_VERSION 1.13.35.2
ENV NGINX_VERSION 1.16.1
ENV CPU_CORE x64

# General Commands
RUN apt update && apt upgrade -y 

# Php-Fpm
RUN apt install -y libcurl4-openssl-dev \
                   libfreetype6-dev \
                   libjpeg62-turbo-dev \
                   libpng-dev \
                   libgd-dev \
                   libmcrypt-dev \
                   libxml2-dev \
                   libxslt-dev \
                   libc-client-dev \
                   libkrb5-dev \
    && rm -r /var/lib/apt/lists/* \               
    && pecl install redis-5.0.2 \
    && pecl install xdebug-2.7.2 \
    && docker-php-ext-enable redis xdebug \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-install -j$(nproc) imap \
    && docker-php-ext-install bcmath \
                              intl \
                              opcache \
                              mysqli \
                              pdo \
                              pdo_mysql \
                              curl \                           
                              mbstring \
                              hash \
                              simplexml \
                              soap \
                              xml \
                              xsl \
                              zip \
                              json
# Php Permissions                              
RUN useradd docker-usr \
    && usermod -aG www-data docker-usr \
    && usermod -aG root www-data
    
#Nginx-ModSecurity-PageSpeedInsight
RUN apt update \ 
    && apt upgrade -y \
    && apt install -y apt-transport-https \
                      apt-utils \
                      autoconf \
                      automake \
                      build-essential \
                      git \
                      libcurl4-openssl-dev \
                      libgeoip-dev \
                      liblmdb-dev \
                      libpcre++-dev \
                      libtool \
                      libxml2-dev \
                      libyajl-dev \
                      pkgconf \
                      wget \
                      zlib1g-dev \
                      libpcre3 \
                      libpcre3-dev \
                      unzip \
                      uuid-dev \
                      libssl-dev
                      
#ModSecurity Install
RUN cd \    
    && git clone --depth 1 -b v3/master --single-branch https://github.com/SpiderLabs/ModSecurity \
    && git clone --depth 1 https://github.com/SpiderLabs/ModSecurity-nginx.git \
    && cd ModSecurity \
    && git submodule init \
    && git submodule update \
    && ./build.sh \
    && ./configure \
    && make \
    && make install
    
#Google PageSpeed Install
RUN cd \
    && wget https://github.com/pagespeed/ngx_pagespeed/archive/v${NPS_VERSION}-stable.zip \
    && unzip v${NPS_VERSION}-stable.zip \
    && cd incubator-pagespeed-ngx-${NPS_VERSION}-stable/ \
    && wget https://dl.google.com/dl/page-speed/psol/${NPS_VERSION}-${CPU_CORE}.tar.gz \
    && tar -xzvf ${NPS_VERSION}-${CPU_CORE}.tar.gz

#Nginx Permissions
RUN useradd -r nginx \    
    && mkdir -p /var/cache/nginx \ 
    && mkdir -p /etc/nginx/modules \
    && chown nginx:root /var/cache/nginx \
    && chown nginx:root /etc/nginx/modules  
    
#Nginx Install
RUN cd \
    && wget http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz \
    && tar -xvzf nginx-${NGINX_VERSION}.tar.gz \
    && cd nginx-${NGINX_VERSION}/ \
    && ./configure --prefix=/etc/nginx --sbin-path=/usr/sbin/nginx --modules-path=/usr/lib/nginx/modules \
    --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log \
    --pid-path=/var/run/nginx.pid --lock-path=/var/run/nginx.lock --http-client-body-temp-path=/var/cache/nginx/client_temp \
    --http-proxy-temp-path=/var/cache/nginx/proxy_temp --http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp \
    --http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp --http-scgi-temp-path=/var/cache/nginx/scgi_temp --user=nginx \
    --group=nginx --with-compat --with-file-aio --with-threads --with-http_addition_module --with-http_auth_request_module \
    --with-http_dav_module --with-http_flv_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_mp4_module \
    --with-http_random_index_module --with-http_realip_module --with-http_secure_link_module --with-http_slice_module \
    --with-http_ssl_module --with-http_stub_status_module --with-http_sub_module --with-http_v2_module --with-mail \
    --with-mail_ssl_module --with-stream --with-stream_realip_module --with-stream_ssl_module --with-stream_ssl_preread_module \
    --with-cc-opt='-g -O2 -fdebug-prefix-map=/data/builder/debuild/nginx-${NPS_VERSION}/debian/debuild-base/nginx-${NPS_VERSION}=. -fstack-protector-strong -Wformat -Werror=format-security -Wp,-D_FORTIFY_SOURCE=2 -fPIC' --with-ld-opt='-Wl,-z,relro -Wl,-z,now -Wl,--as-needed -pie' \
    --add-dynamic-module=$HOME/incubator-pagespeed-ngx-${NPS_VERSION}-stable --add-dynamic-module=$HOME/ModSecurity-nginx \
    && make modules \
    && cp objs/ngx_http_modsecurity_module.so /etc/nginx/modules \
    && cp objs/ngx_pagespeed.so /etc/nginx/modules \
    && make \
    && make install
    
# LetsEncrypt-Certbot Install    
RUN apt install -y certbot

# Tools Install
RUN apt install -y nano htop iputils-ping
    
# Supervisord Install
RUN apt install -y supervisor \
    && mkdir -p /var/log/supervisor
COPY ./supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Cron Install
RUN apt install -y cron 
COPY ./jobs /etc/cron.d/jobs

#Entrypoint
CMD ["/usr/bin/supervisord"]
