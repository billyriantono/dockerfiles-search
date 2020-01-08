FROM debian:jessie
MAINTAINER Sean Johnson <pirogoeth@maio.me>

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential libc6-dev libc-dev-bin curl git libpcre3-dev \
    libssl-dev zlib1g-dev ca-certificates liblzma-dev

RUN gpg --keyserver pgp.mit.edu --recv-key \
    A09CD539B8BB8CBE96E82BDFABD4D3B3F5806B4D \
    4C2C85E705DC730833990C38A9376139A524C53E \
    B0F4253373F8F6F510D42178520A9993A1C052F8 \
    65506C02EFC250F1B7A3D694ECF0E90B2C172083 \
    7338973069ED3F443F4D37DFA64FD5B17ADB39A8 \
    6E067260B83DCF2CA93C566F518509686C7E5E82 \
    573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62

ENV NGINX_VERSION 1.7.8

RUN git config --global http.sslVerify false

RUN curl -SL "http://nginx.org/download/nginx-$NGINX_VERSION.tar.gz" -o nginx.tar.gz \
    && curl -SL "http://nginx.org/download/nginx-$NGINX_VERSION.tar.gz.asc" -o nginx.tar.gz.asc \
    && gpg --verify nginx.tar.gz.asc \
    && mkdir -p /usr/src/nginx \
    && tar xzvpf nginx.tar.gz -C /usr/src/nginx --strip-components=1 \
    && git clone http://github.com/yaoweibin/nginx_tcp_proxy_module.git /usr/src/nginx/nginx_tcp_proxy_module \
    && rm nginx.tar.gz.*

RUN git config --global http.sslVerify true

RUN cd /usr/src/nginx \
    && patch -p1 < /usr/src/nginx/nginx_tcp_proxy_module/tcp.patch \
    && ./configure \
        --user=www-data \
        --group=www-data \
        --prefix=/usr/local/nginx \
        --conf-path=/etc/nginx/nginx.conf \
        --http-log-path=/proc/self/fd/1 \
        --error-log-path=/proc/self/fd/2 \
        --with-http_ssl_module \
        --with-ipv6 \
        --with-pcre-jit \
        --add-module=/usr/src/nginx/nginx_tcp_proxy_module \
    && make -j"$(nproc)" \
    && make install \
    && cd / \
    && rm -rf /usr/src/nginx \
    && chown -R www-data:www-data /usr/local/nginx \
    && { \
        echo; \
        echo '# stay in the foreground so docker can attach'; \
        echo 'daemon off;'; \
       } >> /etc/nginx/nginx.conf \
    && apt-get purge -y --auto-remove build-essential

ENV PATH /usr/local/nginx/sbin:$PATH
WORKDIR /usr/local/nginx/html

# USER www-data

EXPOSE 80 443
VOLUME ["/etc/nginx"]
CMD ["nginx"] 
