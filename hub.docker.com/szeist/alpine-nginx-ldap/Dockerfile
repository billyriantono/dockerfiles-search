FROM alpine:3.3

ENV NGINX_VER=1.9.12
ENV NGINX_LDAP_REV=8517bb0

ENV BUILD_PKGS "curl make gcc g++ openldap-dev autoconf automake gzip libtool linux-headers openssl-dev pcre-dev tar zlib-dev"
ENV RUN_PKGS="libldap openssl pcre zlib bash"

RUN set -x \
  && addgroup -S nginx \
  && adduser -S -G nginx -D -H -s /bin/false nginx \
  && apk add --update ${BUILD_PKGS} ${RUN_PKGS}

RUN mkdir -p /tmp/src/nginx /tmp/src/nginx-auth-ldap \
  && curl -L https://api.github.com/repos/nginx/nginx/tarball/release-${NGINX_VER} | tar xz --strip=1 -C /tmp/src/nginx \
  && curl -L https://api.github.com/repos/kvspb/nginx-auth-ldap/tarball/${NGINX_LDAP_REV} | tar xz --strip=1 -C /tmp/src/nginx-auth-ldap

RUN cd /tmp/src/nginx \
  && ./auto/configure \
    --with-ld-opt="-L /usr/local/lib" \
    --with-threads \
    --with-http_ssl_module \
    --with-http_v2_module \
    --add-module=/tmp/src/nginx-auth-ldap \
    --user=nginx \
    --group=nginx \
    --sbin-path=/usr/sbin/nginx \
    --conf-path=/etc/nginx/nginx.conf \
    --pid-path=/var/run/nginx.pid \
    --error-log-path=/dev/stderr \
    --http-log-path=/dev/stdout \
  && make && make install

RUN apk del --purge ${BUILD_PKGS} && rm -rf /tmp/* /var/tmp/* /var/cache/apk/*

COPY usr/local/sbin/start.sh /usr/local/sbin/start.sh
COPY etc/nginx/nginx.conf /etc/nginx/nginx.conf
COPY etc/nginx/ldap.conf /etc/nginx/ldap.conf

EXPOSE 80 443

CMD "/usr/local/sbin/start.sh"
