FROM ubuntu:14.04
MAINTAINER Matt Ho

RUN apt-get update && apt-get install -y curl

# for 64-bit systems
RUN curl -o /tmp/influxdb_latest_amd64.deb -L http://s3.amazonaws.com/influxdb/influxdb_latest_amd64.deb ; \
	dpkg -i /tmp/influxdb_latest_amd64.deb ; \
	rm -f /tmp/influxdb_latest_amd64.deb

EXPOSE 8083 8086 8090 8099 

VOLUME ["/opt/influxdb/shared/data"]

CMD ["/usr/bin/influxdb", "-config=/opt/influxdb/shared/config.toml", "-stdout=true"]
