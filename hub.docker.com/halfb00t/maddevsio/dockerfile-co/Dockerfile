FROM alpine:3

LABEL maintainer="haist@botsiah.fail"

ENV NGINX_VERSION nginx-1.17.5

RUN apk --update add openssl-dev pcre-dev zlib-dev wget build-base && \
  mkdir -p /tmp/src && \
  cd /tmp/src && \
  # arches officially built by upstream
  set -x \
  && KEY_SHA512="e7fa8303923d9b95db37a77ad46c68fd4755ff935d0a534d26eba83de193c76166c68bfe7f65471bf8881004ef4aa6df3e34689c305662750c0172fca5d8552a *stdin" \
  && apk add --no-cache --virtual .cert-deps \
  openssl \
  && wget -O /tmp/nginx_signing.rsa.pub https://nginx.org/keys/nginx_signing.rsa.pub \
  && if [ "$(openssl rsa -pubin -in /tmp/nginx_signing.rsa.pub -text -noout | openssl sha512 -r)" = "$KEY_SHA512" ]; then \
  echo "key verification succeeded!"; \
  mv /tmp/nginx_signing.rsa.pub /etc/apk/keys/; \
  else \
  echo "key verification failed!"; \
  exit 1; \
  fi && \
  wget https://nginx.org/download/${NGINX_VERSION}.tar.gz && \
  apk del .cert-deps && \
  tar -zxvf ${NGINX_VERSION}.tar.gz && \
  sed -i 's/"Server: nginx" CRLF;/"Server: Botsiah" CRLF;/' /tmp/src/${NGINX_VERSION}/src/http/ngx_http_header_filter_module.c && \
  sed -i 's/"Server: " NGINX_VER CRLF;/"Server: Botsiah" CRLF;/' /tmp/src/${NGINX_VERSION}/src/http/ngx_http_header_filter_module.c && \
  sed -i 's/"Server: " NGINX_VER_BUILD CRLF;/"Server: Botsiah" CRLF;/' /tmp/src/${NGINX_VERSION}/src/http/ngx_http_header_filter_module.c && \
  cd /tmp/src/${NGINX_VERSION} && \
  ./configure \
  --with-http_ssl_module \
  --with-http_gzip_static_module \
  --prefix=/etc/nginx \
  --http-log-path=/var/log/nginx/access.log \
  --error-log-path=/var/log/nginx/error.log \
  --sbin-path=/usr/local/sbin/nginx && \
  make && \
  make install && \
  apk del build-base && \
  rm -rf /tmp/src && \
  rm -rf /var/cache/apk/*

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

VOLUME ["/var/log/nginx"]

WORKDIR /etc/nginx

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
