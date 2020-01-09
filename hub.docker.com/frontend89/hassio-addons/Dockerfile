ARG BUILD_FROM=hassioaddons/base:4.1.1
FROM $BUILD_FROM

ENV LANG C.UTF-8

COPY run.sh /
RUN chmod a+x /run.sh
RUN apk add --update nodejs npm git

VOLUME /config

EXPOSE 3015
CMD [ "/run.sh" ]

ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="NodeJS runner" \
    io.hass.description="NODEJS container running simple nodejs applications" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Bartlomiej Pietrzyk <pietrzyk.bartlomiej@gmail.com>" \
    org.label-schema.description="NODEJS container running simple nodejs applications" \
    org.label-schema.build-date=${BUILD_DATE} \
    org.label-schema.name="NodeJS runner" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.url="https://github.com/frontend89/hassio-addons-nodejs-runner" \
    org.label-schema.usage="https://github.com/frontend89/hassio-addons-nodejs-runner/README.md" \
    org.label-schema.vcs-ref=${BUILD_REF} \
    org.label-schema.vcs-url="https://github.com/frontend89/hassio-addons-nodejs-runner" \
    org.label-schema.vendor="Bartlomiej Pietrzyk"
