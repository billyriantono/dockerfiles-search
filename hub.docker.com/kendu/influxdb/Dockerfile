FROM debian:latest
MAINTAINER Kendu Devops <devops@kendu.si>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get upgrade && apt-get install -y curl apt-transport-https

RUN curl -sL https://repos.influxdata.com/influxdb.key | apt-key add - && \
	. /etc/os-release && \
	test $VERSION_ID="7" && echo "deb https://repos.influxdata.com/debian wheezy stable" | tee /etc/apt/sources.list.d/influxdb.list && \
	test $VERSION_ID="8" && echo "deb https://repos.influxdata.com/debian jessie stable" | tee /etc/apt/sources.list.d/influxdb.list

RUN apt-get update && apt-get install influxdb

RUN apt-get -y autoclean && apt-get -y autoremove && apt-get -y clean

VOLUME /var/opt/influxdb/db

# TCP port 8083 is used for InfluxDB’s Admin panel
# TCP port 8086 is used for client-server communication over InfluxDB’s HTTP API
# TCP ports 8088 and 8091 are required for clustered InfluxDB instances
EXPOSE 8083 8086 8088 8091

CMD [ "/usr/bin/influxd", "-config", "/etc/influxdb/influxdb.conf" ]
