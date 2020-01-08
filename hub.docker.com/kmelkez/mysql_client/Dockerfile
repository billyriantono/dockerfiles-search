FROM debian:wheezy
MAINTAINER Matthieu Keromen <sharoomsorg@gmail.com>
ENV REFRESHED_AT 2015-05-25

ENV TIMEZONE America/Montreal

RUN apt-get update && apt-get install -y \
    mysql-client && \
    echo $TIMEZONE > /etc/timezone && \
    dpkg-reconfigure --frontend noninteractive tzdata

ENV ACTION dump
ENV LOCATION_DIR /var/www
ENV FILE_PREFIX mysql

ADD ./start.sh /start.sh
RUN chmod 755 /start.sh

ENTRYPOINT ["/start.sh"]
