FROM debian:jessie

MAINTAINER Peter Sorowka <sorowka@cybus.io>

COPY . /install
RUN dpkg -i /install/influxdb_*_amd64.deb \
 && cp /install/influxdb.conf /etc/influxdb/ \
 && rm -rf /install

# Admin server WebUI and HTTP API
EXPOSE 8083 8086

#EXPOSE 8090 # Raft port (for clustering, don't expose publicly!)
#EXPOSE 8099 # Protobuf port (for clustering, don't expose publicly!)

VOLUME ["/data"]
ENTRYPOINT ["influxd"]
