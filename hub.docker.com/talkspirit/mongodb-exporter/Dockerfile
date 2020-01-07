FROM quay.io/prometheus/busybox:latest
MAINTAINER  Olivier RICARD <olivier+mongo-exporter@talkspirit.com>

COPY mongodb_exporter /bin/mongodb_exporter

EXPOSE      9216
ENTRYPOINT  [ "/bin/mongodb_exporter" ]
