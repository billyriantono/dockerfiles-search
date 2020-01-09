FROM alpine:3.8
ENV IMAGE_VERSION=1.0.1

LABEL image.version="${IMAGE_VERSION}" \
      image.description="Simple Network Video Recorder for ip-cameras. Docker image based on Alpine Linux." \
      image.date="2018-12-05" \
      maintainer="Evgen Rusakov" \
      url.docker="https://hub.docker.com/r/rev9en/nvr" \
      url.source="https://github.com/revgen/docker-nvr"

ENV NVR_HOME=/var/nvr
ENV NVR_OUTPUT=${NVR_HOME}/output
ENV NVR_LOGS=/var/log/nvr

COPY /root /

RUN apk add --no-cache gettext curl && \
    apk add --no-cache lighttpd && \
    apk add --no-cache ffmpeg mplayer && \
    # Remove mplayer because we need mencoder only
    rm /usr/bin/mplayer && \
    \
    mkdir -p "${NVR_HOME}" && \
    mkdir -p "${NVR_OUTPUT}" && \
    mkdir -p "${NVR_LOGS}" && \
    rm -r /var/www/localhost && \
    chmod +x /entrypoint.sh && \
    chmod +x /usr/local/bin/nvr* && \
    find ${NVR_HOME}/ -name "*.sh" -type f -exec chmod +x "{}" \; && \
    find /usr/lib/nvr/ -name "*.sh" -type f -exec chmod +x "{}" \; && \
    \
    (rm -rf /tmp/* 2>/dev/null || true) && \
    (rm -rf /var/cache/apk/* 2>/dev/null || true)

EXPOSE 80 443

WORKDIR ${NVR_HOME}
VOLUME ${NVR_OUTPUT}

ENTRYPOINT ["/entrypoint.sh"]
