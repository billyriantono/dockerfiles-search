FROM ubuntu:bionic

LABEL maintainer="Stephen Biasotto <sbiasotto@pegtec.com>"

ARG DEBIAN_FRONTEND=noninteractive

ENV LC_ALL=C.UTF-8 \
    LANG=en_US.UTF-8 \
    LANGUAGE=en_US.UTF-8 \
    VERSION=3.10.2
 
WORKDIR /working

ADD run.sh /working/run.sh
ADD docker-healthcheck.sh /working/docker-healthcheck.sh
ADD docker-build.sh /working/docker-build.sh
ADD docker-entrypoint.sh /working/docker-entrypoint.sh

RUN set -ex \
    && chmod 755 /working/run.sh \
    && chmod 755 /working/docker-healthcheck.sh \
    && chmod 755 /working/docker-build.sh \
    && chmod 755 /working/docker-entrypoint.sh \
    && /working/docker-build.sh


VOLUME ["/var/lib/unifi-video"]

# RTMP, RTMPS & RTSP via the controller
EXPOSE 1935/tcp 7444/tcp 7447/tcp

# Inbound Camera Streams & Camera Management (NVR Side)
EXPOSE 6666/tcp 7442/tcp

# UVC-Micro Talkback (Camera Side)
EXPOSE 7004/udp

# HTTP & HTTPS Web UI + API
EXPOSE 7080/tcp 7443/tcp

# Video over HTTP & HTTPS
EXPOSE 7445/tcp 7446/tcp

HEALTHCHECK CMD /working/docker-healthcheck.sh || exit 1

ENTRYPOINT ["/working/docker-entrypoint.sh"]
CMD ["/working/run.sh"]
