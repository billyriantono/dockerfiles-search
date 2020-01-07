FROM kozhin/node

ENV PASSENGER_VERSION="6.0.0" \
    NGINX_VERSION="1.15.7" \
    NGINX_SRC_PATH="/src/nginx" \
    NGINX_PATH="/opt/nginx" \
    PATH=/src/passenger/bin:$PATH

RUN RUBY_LANG="ruby ruby-rake ruby-etc ruby-dev" && \
    PACKAGES="bash curl pcre procps ca-certificates libstdc++ libffi-dev" && \
    BUILD_PACKAGES="linux-headers curl-dev pcre-dev libexecinfo-dev build-base zlib-dev" && \
    apk add --no-cache --update ${RUBY_LANG} ${PACKAGES} ${BUILD_PACKAGES} && \
    gem install rack rake --no-document && \
    mkdir -p /opt /src && \
    cd /src && \
    curl -L http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz | tar -xzf - -C /src && \
    mv nginx-${NGINX_VERSION} nginx && \
    curl -L https://s3.amazonaws.com/phusion-passenger/releases/passenger-${PASSENGER_VERSION}.tar.gz | tar -xzf - -C /src && \
    mv passenger-${PASSENGER_VERSION} passenger && \
    export EXTRA_PRE_CFLAGS='-O' EXTRA_PRE_CXXFLAGS='-O' EXTRA_LDFLAGS='-lexecinfo' && \
    passenger-install-nginx-module --auto \
        --prefix=${NGINX_PATH} \
        --nginx-source-dir=${NGINX_SRC_PATH} \
        --extra-configure-flags="\
        --with-file-aio \
        --with-http_addition_module \
        --with-http_auth_request_module \
        --with-http_dav_module \
        --with-http_flv_module \
        --with-http_gunzip_module \
        --with-http_gzip_static_module \
        --with-http_mp4_module \
        --with-http_random_index_module \
        --with-http_realip_module \
        --with-http_secure_link_module \
        --with-http_slice_module \
        --with-http_ssl_module \
        --with-http_stub_status_module \
        --with-http_sub_module \
        --with-http_v2_module \
        --with-ipv6 \
        --with-mail \
        --with-mail_ssl_module \
        --with-stream \
        --with-stream_ssl_module \
        --with-threads" && \
    passenger-config build-native-support && \
    ln -s ${NGINX_PATH}/sbin/nginx /usr/sbin/nginx && \
    ln -s ${NGINX_PATH} /etc/nginx && \
    chmod o+x /root && \
    ln -sf /dev/stdout ${NGINX_PATH}/logs/access.log && \
    ln -sf /dev/stderr ${NGINX_PATH}/logs/error.log && \
    rm -rf /tmp/* && \
    mv /src/passenger/src/ruby_supportlib /tmp && \
    mv /src/passenger/src/nodejs_supportlib /tmp && \
    mv /src/passenger/src/helper-scripts /tmp && \
    rm -rf /src/passenger/src/* && \
    mv /tmp/* /src/passenger/src/ && \
    passenger-config validate-install --auto && \
    addgroup -g 9999 app && \
    adduser -D -u 9999 -G app app && \
    apk del ${BUILD_PACKAGES} && \
    rm -rf /var/cache/apk/* /tmp/* /src/nginx /src/passenger/doc

COPY nginx.conf /etc/nginx/conf/

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
