FROM ubuntu:trusty
MAINTAINER Markus Mayer <m.mayer@everybag.de>

ENV DEBIAN_FRONTEND noninteractive
ENV NGINX_VERSION 1.9.15
ENV NPS_VERSION 1.11.33.2

# From instructions here: https://github.com/pagespeed/ngx_pagespeed

# Install dependencies
# Download ngx_pagespeed
# Download nginx
# Build nginx
# Cleanup

RUN apt-get update -qq \
	&& apt-get install -yqq build-essential zlib1g-dev libpcre3 libpcre3-dev openssl libssl-dev libperl-dev wget ca-certificates logrotate \
	&& (wget -qO - https://github.com/pagespeed/ngx_pagespeed/archive/v$NPS_VERSION-beta.tar.gz | tar zxf - -C /tmp) \
	&& (wget -qO - https://dl.google.com/dl/page-speed/psol/$NPS_VERSION.tar.gz | tar zxf - -C /tmp/ngx_pagespeed-$NPS_VERSION-beta/) \
	&& (wget -qO - http://nginx.org/download/nginx-$NGINX_VERSION.tar.gz | tar zxf - -C /tmp) \
	&& cd /tmp/nginx-$NGINX_VERSION \
	&& ./configure --prefix=/etc/nginx/ --sbin-path=/usr/sbin/nginx --add-module=/tmp/ngx_pagespeed-$NPS_VERSION-beta --with-http_ssl_module --with-http_v2_module --with-http_stub_status_module \
	&& make install \
	&& rm -Rf /tmp/* \
	&& apt-get purge -yqq wget build-essential \
	&& apt-get autoremove -yqq \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*

WORKDIR /etc/nginx/
ENTRYPOINT ["/usr/sbin/nginx"]

# Configure nginx
RUN mkdir /var/ngx_pagespeed_cache
RUN chmod 777 /var/ngx_pagespeed_cache
COPY nginx.conf /etc/nginx/conf/nginx.conf
COPY sites-enabled /etc/nginx/sites-enabled
