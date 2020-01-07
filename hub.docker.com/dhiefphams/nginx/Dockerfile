FROM ubuntu:xenial
MAINTAINER Tinpee <tinpee.dev@gmail.com>

ENV NPS_VERSION 1.11.33.4
ENV NGINX_VERSION 1.11.12
ENV OPENSSL_VERSION 1_1_0e

RUN rm -rf /var/lib/apt/lists/ \
	&& apt-get update \
	&& apt-get install -y dpkg-dev build-essential zlib1g-dev libpcre3 libpcre3-dev wget

RUN echo "deb http://nginx.org/packages/mainline/ubuntu/ xenial nginx" >> /etc/apt/sources.list \
	&& echo "deb-src http://nginx.org/packages/mainline/ubuntu/ xenial nginx" >> /etc/apt/sources.list \
	&& apt-key adv --keyserver keyserver.ubuntu.com --recv-keys ABF5BD827BD9BF62 \
	&& apt-get update \
	&& apt-get install nginx

RUN cd /tmp \
	&& wget https://github.com/pagespeed/ngx_pagespeed/archive/latest-stable.tar.gz \
	&& tar -zvxf latest-stable.tar.gz \
	&& cd ngx_pagespeed-latest-stable/ \
	&& wget https://dl.google.com/dl/page-speed/psol/${NPS_VERSION}.tar.gz \
	&& tar -xzvf ${NPS_VERSION}.tar.gz \
	&& cd /tmp \
	&& wget https://github.com/openssl/openssl/archive/OpenSSL_${OPENSSL_VERSION}.tar.gz\
	&& tar -xzvf OpenSSL_${OPENSSL_VERSION}.tar.gz \
	&& cd /tmp \
	&& wget http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz \
	&& tar -xvzf nginx-${NGINX_VERSION}.tar.gz \
	&& cd nginx-${NGINX_VERSION}/ \
	&& ./configure  \
		--add-module=/tmp/ngx_pagespeed-latest-stable ${PS_NGX_EXTRA_FLAGS} \
		--prefix=/etc/nginx \
		--sbin-path=/usr/sbin/nginx \
		--conf-path=/etc/nginx/nginx.conf \
		--error-log-path=/var/log/nginx/error.log \
		--http-log-path=/var/log/nginx/access.log \
		--pid-path=/var/run/nginx.pid \
		--lock-path=/var/run/nginx.lock \
		--http-client-body-temp-path=/var/cache/nginx/client_temp \
		--http-proxy-temp-path=/var/cache/nginx/proxy_temp \
		--http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp \
		--http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp \
		--http-scgi-temp-path=/var/cache/nginx/scgi_temp \
		--user=nginx \
		--group=nginx \
		--with-http_ssl_module --with-openssl=/tmp/openssl-OpenSSL_${OPENSSL_VERSION} \
		--with-http_realip_module \
		--with-http_addition_module \
		--with-http_sub_module \
		--with-http_dav_module \
		--with-http_flv_module \
		--with-http_mp4_module \
		--with-http_gunzip_module \
		--with-http_gzip_static_module \
		--with-http_random_index_module \
		--with-http_secure_link_module \
		--with-http_stub_status_module \
		--with-http_auth_request_module \
		--with-threads \
		--with-stream \
		--with-stream_ssl_module \
		--with-http_slice_module \
		--with-mail \
		--with-mail_ssl_module \
		--with-file-aio \
		--with-http_v2_module \
		--with-ipv6 \
		--with-stream_realip_module \
	&& make \
	&& make install \
	&& cd \
	&& rm -rf /tmp/*

RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80 443
VOLUME /etc/nginx

CMD [ "nginx", "-g", "daemon off;" ]