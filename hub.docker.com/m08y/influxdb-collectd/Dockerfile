FROM debian:stretch-slim

LABEL maintainer="Aneurin Price adp@nyeprice.space"

RUN apt-get update && apt-get -y install apt-utils influxdb
COPY * /etc/influxdb/
CMD influxd
EXPOSE 25826
EXPOSE 8086
EXPOSE 8081
