FROM alpine:3.4

MAINTAINER 8 Wire Digital <info@8wiredigital.co.nz>

ENV NPS_VERSION=1.9.32.10 \
    NGINX_VERSION=1.10.1 \
    NGINX_USER=www \
    NGINX_USERID=9999 \
    NGINX_CONF_DIR=/etc/nginx \
    NGINX_LOG_DIR=/var/log/nginx \
    SRC_DIR=/tmp/src \
    BUILD_DEPS="gcc \
        ca-certificates \
        libc-dev \
		make \
		openssl-dev \
		pcre-dev \
		zlib-dev \
		linux-headers \
		gnupg" \
    PERSISTANT_DEPS="openssl \
        pcre \
        zlib"

#set up user
RUN adduser -D -u ${NGINX_USERID} ${NGINX_USER}

RUN apk --update add ${PERSISTANT_DEPS} ${BUILD_DEPS} \
    && update-ca-certificates \
    && mkdir -p ${SRC_DIR} \
    && cd ${SRC_DIR} \
    && wget http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz \
    && tar -zxvf nginx-${NGINX_VERSION}.tar.gz \
    #&& wget https://github.com/nbs-system/naxsi/archive/0.54.tar.gz \
    #&& tar -zxvf 0.54.tar.gz \
    ## installing pagespeed -not working
    # wget https://github.com/pagespeed/ngx_pagespeed/archive/release-${NPS_VERSION}-beta.zip \
    # unzip release-${NPS_VERSION}-beta.zip \
    # wget https://dl.google.com/dl/page-speed/psol/${NPS_VERSION}.tar.gz \
    # tar -xzvf ${NPS_VERSION}.tar.gz -C ngx_pagespeed-release-${NPS_VERSION}-beta \
    && cd ${SRC_DIR}/nginx-${NGINX_VERSION} \
    && ./configure \
        --prefix=${NGINX_CONF_DIR} \
        --conf-path=${NGINX_CONF_DIR}/nginx.conf \
        --error-log-path=${NGINX_LOG_DIR}/error.log \
        --http-log-path=${NGINX_LOG_DIR}/access.log  \
        --user=${NGINX_USER} \
        --group=${NGINX_USER} \
        --sbin-path=/usr/sbin/nginx \
        #--add-module=${SRC_DIR}/naxsi-0.54/naxsi_src/ \
        #--add-module=${SRC_DIR}/ngx_pagespeed-release-${NPS_VERSION}-beta \
        --with-http_ssl_module \
        --with-http_gzip_static_module \
        --with-http_realip_module \
        --without-mail_pop3_module \
        --without-mail_smtp_module \
        --without-mail_imap_module \

    && make \
    && make install \
    && strip -s /usr/sbin/nginx \
    && apk del ${BUILD_DEPS} \
    && apk add ${PERSISTANT_DEPS} \
    && rm -rf ${SRC_DIR} \
    && rm -rf /var/cache/apk/*

# forward request and error logs to docker log collector
# RUN ln -sf /dev/stdout $NGINX_LOG_DIR/access.log
# RUN ln -sf /dev/stderr $NGINX_LOG_DIR/error.log

#setup default nginx.conf
RUN mkdir ${NGINX_CONF_DIR}/conf.d \
    && mkdir ${NGINX_CONF_DIR}/sites-enabled \
    && mkdir ${NGINX_CONF_DIR}/sites-available \
    && mkdir ${NGINX_CONF_DIR}/templates


COPY conf/nginx.conf ${NGINX_CONF_DIR}/
COPY conf/mime.types ${NGINX_CONF_DIR}/
COPY conf/conf.d ${NGINX_CONF_DIR}/conf.d
COPY templates ${NGINX_CONF_DIR}/templates
COPY errors ${NGINX_CONF_DIR}/errors


VOLUME ["$NGINX_LOG_DIR"]

WORKDIR /etc/nginx

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
