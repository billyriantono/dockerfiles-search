FROM alpine:3.10

LABEL maintainer="Benjamin Hubert <docker@benjaminhubert.at>"

ENV NGINX_VERSION   1.16.0
ENV PACKAGE_VERSION 2

RUN apk add --no-cache nginx=${NGINX_VERSION}-r${PACKAGE_VERSION} \
                       nginx-mod-stream=${NGINX_VERSION}-r${PACKAGE_VERSION} \
                       nginx-mod-http-geoip2=${NGINX_VERSION}-r${PACKAGE_VERSION} \
 && mkdir -p /run/nginx \
 # Make sure that stream module gets loaded before geoip2 module
 # See https://github.com/leev/ngx_http_geoip2_module/issues/42
 && mv /etc/nginx/modules/stream.conf /etc/nginx/modules/00-stream.conf \
 && mv /etc/nginx/modules/http_geoip2.conf /etc/nginx/modules/90-http_geoip2.conf \
 # forward request and error logs to docker log collector
 && ln -sf /dev/stdout /var/log/nginx/access.log \
 && ln -sf /dev/stderr /var/log/nginx/error.log

ADD nginx.conf /etc/nginx/nginx.conf

EXPOSE 80
EXPOSE 443

STOPSIGNAL SIGTERM

CMD ["nginx", "-g", "daemon off;"]

