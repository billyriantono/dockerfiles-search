# nginx

FROM ubuntu:trusty
MAINTAINER Ramon Torres <ramon.torres@edgebound.com>

ENV NGINX_VERSION 1.9.3
ENV NPS_VERSION 1.9.32.6

RUN \
	apt-get update && apt-get install -y build-essential zlib1g-dev libpcre3 libpcre3-dev unzip wget libssl-dev && \
	wget http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz -O /tmp/nginx.tar.gz && tar -xf /tmp/nginx.tar.gz -C /tmp/ && \
	wget https://github.com/pagespeed/ngx_pagespeed/archive/release-${NPS_VERSION}-beta.zip -P /tmp/ && \
	unzip /tmp/release-${NPS_VERSION}-beta.zip -d /tmp/ && cd /tmp/ngx_pagespeed-release-${NPS_VERSION}-beta/ && \
	wget https://dl.google.com/dl/page-speed/psol/${NPS_VERSION}.tar.gz && tar -xzvf ${NPS_VERSION}.tar.gz && \
	cd /tmp/nginx-${NGINX_VERSION} && mkdir -p /var/lib/nginx && ./configure --add-module=/tmp/ngx_pagespeed-release-${NPS_VERSION}-beta --prefix=/etc/nginx --sbin-path=/usr/sbin/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --pid-path=/var/run/nginx.pid --lock-path=/var/run/nginx.lock --http-client-body-temp-path=/var/cache/nginx/client_temp --http-proxy-temp-path=/var/cache/nginx/proxy_temp --http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp --http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp --http-scgi-temp-path=/var/cache/nginx/scgi_temp --user=nginx --group=nginx --with-http_ssl_module --with-http_realip_module --with-http_addition_module --with-http_sub_module --with-http_dav_module --with-http_flv_module --with-http_mp4_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_random_index_module --with-http_secure_link_module --with-http_stub_status_module --with-http_auth_request_module --with-mail --with-mail_ssl_module --with-file-aio --with-http_spdy_module --with-ipv6 --with-threads --with-stream --with-stream_ssl_module && \
	make && make install && apt-get clean && rm -rf /var/cache/apt/* /var/lib/apt/lists/* /tmp/* && \
	echo "\ndaemon off;" >> /etc/nginx/nginx.conf && chown -R www-data:www-data /var/lib/nginx

# define mountable directories
VOLUME ["/etc/nginx/sites-enabled", "/etc/nginx/certs", "/etc/nginx/conf.d", "/var/log/nginx", "/var/www/html"]

EXPOSE 80/tcp 443/tcp

WORKDIR /etc/nginx
CMD ["nginx"]
