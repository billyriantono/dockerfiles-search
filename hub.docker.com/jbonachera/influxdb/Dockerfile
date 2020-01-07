FROM jbonachera/arch
ENV VERSION=1.0.2
RUN curl -sL https://dl.influxdata.com/influxdb/releases/influxdb-${VERSION}_linux_amd64.tar.gz | tar -xz --strip=2 --show-transformed-names -v -f -  -C / && \
    rm -f /var/tmp/influxdb.tgz && \ 
    useradd -r influxdb -d /var/lib/influxdb && \
    chown -R influxdb: /var/lib/influxdb
VOLUME /var/lib/influxdb
USER influxdb
EXPOSE 8086
CMD /usr/bin/influxd
