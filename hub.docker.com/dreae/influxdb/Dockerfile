FROM ubuntu:14.04

MAINTAINER Dreae <thedreae@gmail.com>

RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y wget

RUN wget https://s3.amazonaws.com/influxdb/influxdb_0.8.8_amd64.deb
RUN dpkg -i influxdb_0.8.8_amd64.deb

CMD ["/usr/bin/influxdb", "--config=/opt/influxdb/conf/config.toml"]
