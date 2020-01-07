FROM alpine:edge

MAINTAINER Igor Ilic

ENV NGINX_VERSION nginx-1.13.5

RUN   apk upgrade && \
      apk update && \
      apk add --no-cache --virtual .build-deps \
      openssl-dev \
      libc-dev \
      make \
      zlib-dev \
      libxslt-dev \
      gd-dev \
      bash \
      nodejs-npm \
      gcc \
      yarn \
      linux-headers \
      gnupg \
      pcre-dev \
      wget \
      python2 \
      python \
      build-base && \
      python -m ensurepip && \
      rm -r /usr/lib/python*/ensurepip && \
      pip install --upgrade pip setuptools && \
      mkdir -p /tmp/src && \
      cd /tmp/src && \
      wget http://nginx.org/download/${NGINX_VERSION}.tar.gz && \
      tar -zxvf ${NGINX_VERSION}.tar.gz && \
      cd /tmp/src/${NGINX_VERSION} && \
      ./configure \
          --with-http_ssl_module \
          --with-http_gzip_static_module \
          --conf-path=/etc/nginx/nginx.conf \
          --prefix=/etc/nginx \
          --http-log-path=/var/log/nginx/access.log \
          --error-log-path=/var/log/nginx/error.log \
          --sbin-path=/usr/local/sbin/nginx && \
      make && \
      make install && \
      apk del build-base && \
      apk del .build-deps && \
      rm -rf /tmp/src && \
      rm -rf /root/.cache && \
      rm -rf /var/cache/apk/*

COPY nginx.conf /etc/nginx/nginx.conf
COPY nginx.default.conf /etc/nginx/conf.d/default.conf

EXPOSE 8080 443

STOPSIGNAL SIGTERM

CMD ["nginx", "-g", "daemon off;"]
