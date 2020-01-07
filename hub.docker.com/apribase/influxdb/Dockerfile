FROM apribase/debian-jp
MAINTAINER apribase

# Install InfluxDB
RUN apt-get update
RUN wget http://s3.amazonaws.com/influxdb/influxdb_latest_amd64.deb
RUN dpkg -i ./influxdb_latest_amd64.deb
RUN rm -f ./influxdb_latest_amd64.deb
RUN apt-get clean

EXPOSE 8083 8084 8086
VOLUME ["/data"]
CMD ["/usr/bin/influxdb", "-config=/opt/influxdb/shared/config.toml"]
