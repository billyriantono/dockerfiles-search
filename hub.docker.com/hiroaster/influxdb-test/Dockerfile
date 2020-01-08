FROM ubuntu
MAINTAINER Wenyang <fengwenyang@gmail.com>
# Install InfluxDB
ENV INFLUXDB_VERSION 0.10.3-1
COPY influxdb_${INFLUXDB_VERSION}_amd64.deb  /tmp/influxdb_${INFLUXDB_VERSION}_amd64.deb
COPY run.sh /tmp/run.sh
RUN dpkg -i /tmp/influxdb_${INFLUXDB_VERSION}_amd64.deb 

EXPOSE 8083

EXPOSE 8086

VOLUME ["/data"]

ENTRYPOINT ["/tmp/run.sh"]
