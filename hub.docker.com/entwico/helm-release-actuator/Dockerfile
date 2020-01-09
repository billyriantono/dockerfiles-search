FROM andrexus/baseimage

WORKDIR /srv

ARG APP_VERSION=0.1.1
ARG DOWNLOAD_URL=https://github.com/entwico/helm-release-actuator/releases/download/v$APP_VERSION/helm-release-actuator-linux-amd64

LABEL maintainer="Andrew Tarasenko andrexus@gmail.com"

RUN wget -q $DOWNLOAD_URL -O /srv/helm-release-actuator && \
    chmod +x /srv/helm-release-actuator && \
    chown -R app:app /srv && \
    ln -s /srv/helm-release-actuator /usr/bin/helm-release-actuator

USER app

CMD ["helm-release-actuator", "upgrade"]
