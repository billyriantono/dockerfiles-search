FROM debian:jessie

LABEL maintainer="amitrajput123.ar@gmail.com"

# Set the env variable DEBIAN_FRONTEND to noninteractive
ENV DEBIAN_FRONTEND noninteractive

ENV NGINX_VERSION=1.12.1 \
		NPS_RELEASE_NUMBER=1.12.34.2-

ENV NPS_VERSION=${NPS_RELEASE_NUMBER}stable
		#PS_NGX_EXTRA_FLAGS="--with-cc=/usr/lib/gcc-mozilla/bin/gcc  --with-ld-opt=-static-libstdc++"

RUN apt-get update \
	&& apt-get -y upgrade \
	&& apt-get -y install \
    sudo \
    bash-completion \
    emacs24-nox \
    curl \
    wget \
    inetutils-ping \
    dnsutils \
    netcat \
    lsof \
    net-tools \
	build-essential \
	gcc-4.9 \
	g++-4.9 \
	libpcre3 \
	libpcre3-dev \
	libpcre++-dev \
	libssl-dev \
	checkinstall \
	zlib1g-dev \
	unzip \
	libxml2 \
	libxslt-dev \
	libssl-dev \
	libgd2-xpm-dev \
	libgeoip-dev \
	&& apt-get -y clean

#	get nps module and unzip into folder $NPS_VERSION
RUN wget https://github.com/pagespeed/ngx_pagespeed/archive/v${NPS_VERSION}.zip \
  && unzip v${NPS_VERSION}.zip \
  && echo "NPS_RELEASE_NUMBER" ${NPS_RELEASE_NUMBER};

# extract and create the binary for NPS using the format_binary_url.sh script
RUN cd ngx_pagespeed-${NPS_VERSION}/ \
  && psol_url=https://dl.google.com/dl/page-speed/psol/${NPS_RELEASE_NUMBER}.tar.gz \
     [ -e scripts/format_binary_url.sh ] && exec_cmd=`/bin/sh ./scripts/format_binary_url.sh PSOL_BINARY_URL` \
     && psol_url=$exec_cmd \
  && wget ${psol_url} \
  && tar -xzvf $(basename ${psol_url}); # extracts to ngx_pagespeed-${NPS_VERSION}/psol/

#download nginx
RUN wget http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz \
	&& tar -xvzf nginx-${NGINX_VERSION}.tar.gz

# build nginx with config options
RUN cd nginx-${NGINX_VERSION}/ \
	&& echo "BUILDING pagespeed module" \
	&& ./configure  \
	--prefix=/etc/nginx \
  --sbin-path=/usr/sbin/nginx \
  --modules-path=/usr/lib64/nginx/modules \
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
  --with-http_ssl_module \
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
  --with-http_xslt_module=dynamic \
  --with-http_image_filter_module=dynamic \
  --with-http_geoip_module=dynamic \
  --with-threads \
  --with-stream \
  --with-stream_ssl_module \
  --with-stream_ssl_preread_module \
  --with-stream_realip_module \
  --with-stream_geoip_module=dynamic \
  --with-http_slice_module \
  --with-mail \
  --with-mail_ssl_module \
  --with-compat \
  --with-file-aio \
  --with-ipv6 \
  --with-http_v2_module \
  --add-module=/ngx_pagespeed-${NPS_VERSION} ${PS_NGX_EXTRA_FLAGS} \
	&& make \
	&& make install;

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
	&& ln -sf /dev/stderr /var/log/nginx/error.log

RUN useradd nginx

RUN mkdir -p /var/cache/nginx

COPY nginx.conf /etc/nginx/nginx.conf
COPY nginx.vh.default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

STOPSIGNAL SIGTERM

CMD ["nginx", "-g", "daemon off;"]