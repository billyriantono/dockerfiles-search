FROM alpine:3.4

RUN addgroup -S nginx && \
    adduser -D -S -h /var/cache/nginx -s /sbin/nologin -G nginx nginx

RUN apk --no-cache --update add nginx curl tar
RUN curl -sL https://github.com/alerta/angular-alerta-webui/tarball/master | tar -xzv
RUN mv alerta-angular-alerta-webui-*/app /app

ENV PROVIDER basic
ENV ENDPOINT /api

ADD config.js.sh /config.js.sh
ADD nginx.conf /nginx.conf

EXPOSE 80
CMD /config.js.sh && nginx -c /nginx.conf
