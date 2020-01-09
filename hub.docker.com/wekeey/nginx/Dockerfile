FROM alpine:latest
MAINTAINER WeKeey <wekeey@mxw.me>

ENV TIMEZONE Asia/Shanghai
ENV ERROR_LOG_FILE /data/log/nginx/error.log warn;
ENV ACCESS_LOG_FILE /data/log/nginx/access.log main;
ENV VHOST_FILE /data/xconfig/vhost/*.conf;

RUN apk --update add nginx tzdata \
    && cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime \
    && mkdir -p /run/nginx /data/log/nginx \
    && apk del tzdata \
    && sed -i "s|error_log .*|error_log ${ERROR_LOG_FILE}|" /etc/nginx/nginx.conf \
    && sed -i "s|access_log .*|access_log ${ACCESS_LOG_FILE}|" /etc/nginx/nginx.conf \
    && rm -rf /var/cache/apk/*

EXPOSE 80

STOPSIGNAL SIGTERM

CMD ["nginx", "-g", "daemon off;"]
