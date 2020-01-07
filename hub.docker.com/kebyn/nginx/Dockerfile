FROM alpine:latest
MAINTAINER kebyn <kebyn@sina.com>

ENV LANG C.UTF-8
ENV TZ Asia/Shanghai

RUN set -ex \
  && apk add --no-cache nginx perl \
  && mkdir /run/nginx

COPY default.conf /etc/nginx/conf.d/default.conf
COPY entrypoint.sh /
COPY htpasswd /
EXPOSE 80
STOPSIGNAL SIGTERM

CMD ["/entrypoint.sh"]
