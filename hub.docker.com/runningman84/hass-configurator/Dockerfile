FROM causticlab/hass-configurator-docker:0.3.5-x86_64
LABEL maintainer="Philipp Hellmich <phil@hellmi.de>"
LABEL Description="Home Assistant Configurator"

ARG TIMEZONE=Europe/Paris
ARG UID=1000
ARG GUID=1000

RUN apk add --no-cache tini && \
    addgroup -g ${GUID} hass && \
    adduser -D -G hass -s /bin/sh -u ${UID} hass

ENTRYPOINT ["/sbin/tini", "--"]

CMD [ "/app/run.sh" ]
