FROM oskarirauta/alpine:glibc

VOLUME /config
VOLUME /transcode
VOLUME /data

ENV ADVERTISE_IP=""
ENV ALLOWED_NETWORKS=""
ENV PLEX_UID=""
ENV PLEX_GID=""
ENV PLEX_CLAIM=""
ENV VERSION_TAG="public"

RUN apk add --no-cache \
     dcron \
     patchelf \
     openssl \
     file \
     ca-certificates \
     wget \
     tzdata \
     xmlstarlet \
     util-linux \
     bash \
     curl \
     shadow \
     xz \
     binutils

RUN addgroup -S -g 2001 media
RUN adduser -SH -u 1001 -G media -s /sbin/nologin -h /config plex

RUN update-ca-certificates \
 && chmod 777 /tmp \
 && mkdir -p /etc/scripts

COPY scripts/plex-common.sh /etc/scripts/plex-common.sh
COPY scripts/healthcheck.sh /etc/scripts/healthcheck.sh
COPY scripts/installBinary.sh /etc/scripts/installBinary.sh
COPY init/plex /etc/init.d/plex
COPY config/root /etc/crontabs/root

RUN chmod +x /etc/scripts/plex-common.sh \
 && chmod +x /etc/scripts/healthcheck.sh \
 && chmod +x /etc/scripts/installBinary.sh \
 && chmod +x /etc/init.d/plex

RUN rc-update add plex default \
 && rc-update add dcron default

RUN rm -rf /var/cache/apk/** \
 && rm -rf /tmp/**
