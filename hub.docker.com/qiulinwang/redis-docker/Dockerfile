FROM ubuntu:12.04
MAINTAINER QiuLin Wang <wangql@fuyinshidai.com>
ENV REFRESHED_AT 2015-01-15

RUN apt-get -yqq update
RUN apt-get -yqq install redis-server

VOLUME [ "/etc/redis", "/var/lib/redis", "/var/log/redis/" ]

ADD conf/entrypoint.sh /opt/sbin/entrypoint.sh
RUN chmod +x /opt/sbin/entrypoint.sh

EXPOSE 6379

ENTRYPOINT [ "/opt/sbin/entrypoint.sh" ]
