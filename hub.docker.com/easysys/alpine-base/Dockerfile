FROM alpine:3.2
MAINTAINER easySYS <info@easysys.com>

# Add s6-overlay
ENV S6_OVERLAY_VERSION v1.12.0.0

ADD https://github.com/just-containers/s6-overlay/releases/download/${S6_OVERLAY_VERSION}/s6-overlay-amd64.tar.gz /tmp/s6-overlay.tar.gz
RUN tar xvfz /tmp/s6-overlay.tar.gz -C /

ENTRYPOINT ["/init"]
CMD []
