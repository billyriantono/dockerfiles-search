FROM alpine:3.7 as downloader
ENV VERSION=0.1.0
WORKDIR /tmp
RUN apk add --no-cache gzip tar curl ca-certificates && \
    curl -L --output exporter.tar.gz https://github.com/carlpett/influxdb_stats_exporter/releases/download/v${VERSION}/influxdb_stats_exporter-${VERSION}.linux-amd64.tar.gz && \
    tar --strip-components=1 -xzvf  exporter.tar.gz

FROM scratch
COPY --from=downloader /tmp/influxdb_stats_exporter /
EXPOSE 9424
USER 65534
ENTRYPOINT ["/influxdb_stats_exporter"]
