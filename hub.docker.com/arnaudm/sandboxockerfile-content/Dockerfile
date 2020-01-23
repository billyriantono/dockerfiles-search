FROM buildpack-deps:jessie-curl
MAINTAINER Arkka Dhiratara <arkka.d@gmail.com>

RUN gpg \
    --keyserver hkp://ha.pool.sks-keyservers.net \
    --recv-keys 05CE15085FC09D18E99EFB22684A14CF2582E0C5

ENV INFLUXDB_VERSION 0.13.0
RUN wget -q https://dl.influxdata.com/influxdb/releases/influxdb_${INFLUXDB_VERSION}_amd64.deb.asc && \
    wget -q https://dl.influxdata.com/influxdb/releases/influxdb_${INFLUXDB_VERSION}_amd64.deb && \
    gpg --batch --verify influxdb_${INFLUXDB_VERSION}_amd64.deb.asc influxdb_${INFLUXDB_VERSION}_amd64.deb && \
    dpkg -i influxdb_${INFLUXDB_VERSION}_amd64.deb && \
    rm -f influxdb_${INFLUXDB_VERSION}_amd64.deb*
COPY types.db /usr/share/collectd/types.db
COPY influxdb.conf /etc/influxdb/influxdb.conf

# Admin server WebUI
EXPOSE 8083

# HTTP API
EXPOSE 8086

# COLLECTD
EXPOSE 8096/udp

# GRAPHITE
EXPOSE 2003

VOLUME /var/lib/influxdb

COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
CMD ["influxd"]
