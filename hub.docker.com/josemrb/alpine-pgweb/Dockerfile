FROM josemrb/alpine-supervisord
MAINTAINER Jose Miguel Rivero Bruno <work@josemrb.com>

ENV PGWEB_VERSION 0.9.8

ADD https://github.com/sosedoff/pgweb/releases/download/v$PGWEB_VERSION/pgweb_linux_amd64.zip /tmp/

RUN \
  cd /tmp && \
  unzip pgweb_linux_amd64.zip && \
  mv pgweb_linux_amd64 /usr/bin/pgweb && \
  rm -f pgweb_linux_amd64.zip

COPY pgweb.conf /etc/supervisor/conf.d/pgweb.conf

ENV PGWEB_BIND 0.0.0.0
ENV PGWEB_PORT 8081

EXPOSE 8081
