FROM buildpack-deps:jessie-curl

RUN curl -OL https://s3.amazonaws.com/influxdb/influxdb_latest_amd64.deb \ 
  && dpkg -i influxdb_latest_amd64.deb \ 
  && rm influxdb_latest_amd64.deb

RUN mkdir -p /etc/opt/influxdb \
  && mkdir -p /var/run/influxdb

ADD influxdb_config /etc/opt/influxdb/influxdb.conf

ADD docker-entrypoint.sh /

EXPOSE 8083
EXPOSE 8086

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["influxd"]
