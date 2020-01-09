FROM openjdk:8-jre-alpine

MAINTAINER "HMCTS Team <https://github.com/hmcts>"
LABEL maintainer = "HMCTS Team <https://github.com/hmcts>"

WORKDIR /opt/app
COPY docmosis/docmosisTornado2.6.war .

WORKDIR /tmp/templates
COPY templates/* ./

WORKDIR /tmp/working

RUN apk add --no-cache \
    dumb-init \
    openjdk8 \
    libreoffice \
    libreoffice-base \
    libreoffice-lang-de \
    mesa-gl \
    ttf-freefont

HEALTHCHECK --interval=10s --timeout=10s --retries=10 CMD http_proxy="" curl --silent --fail http://localhost:80/rs/status

EXPOSE 80

ENTRYPOINT exec java ${JAVA_OPTS} -Dlog.level=DEBUG -Dport=80 -jar "/opt/app/docmosisTornado2.6.war"
