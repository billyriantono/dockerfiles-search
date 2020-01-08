FROM phusion/baseimage:0.9.19
MAINTAINER Steven Schneider <stschn@microsoft.com>

RUN apt-get update &&\
    apt-get -y upgrade

RUN curl -O https://dl.influxdata.com/telegraf/releases/telegraf_1.2.1_amd64.deb
RUN dpkg -i telegraf_1.2.1_amd64.deb

ENV SQL_HOSTNAME empty
ENV SQL_USERNAME sa
ENV SQL_PASSWORD nopass
ENV SQL_SERVER_PORT 1433

ENV INFLUX_DB_SERVER  127.0.0.1
ENV INFLUX_DB_PORT 8086

ENV POLL_INTERVAL 5s

ADD telegraf.conf /etc/telegraf/telegraf-template.conf

RUN mkdir -p /etc/service/telegraf
ADD run-telegraf.sh /etc/service/telegraf/run
RUN chmod +x /etc/service/telegraf/run


ENV HOME /root
CMD ["/sbin/my_init"]

