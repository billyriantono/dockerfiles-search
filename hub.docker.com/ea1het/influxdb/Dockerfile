FROM alpine:3.9
MAINTAINER Jonathan Gonzalez j@0x30.io @EA1HET

ARG BUILD_DATE
ARG VCS_REF
ARG VERSION

LABEL maintainer="Jonathan Gonzalez <j@0x30.io>" \
      org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="InfluxDB time series database" \
      org.label-schema.description="This project builds InfluxDB server container." \
      org.label-schema.url="https://hub.docker.com/r/ea1het/influxdb" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://hub.docker.com/r/ea1het/influxdb" \
      org.label-schema.version=$VERSION \
      org.label-schema.schema-version="1.0"

RUN apk --no-cache add influxdb

VOLUME ["/var/lib/influxdb"]
EXPOSE 8083 8086 8088 

ENV PATH=/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:$PATH

WORKDIR /etc/influxdb
COPY . /etc/influxdb

ENTRYPOINT ["influxd"]
CMD ["run", "-config", "influxdb.conf"]
