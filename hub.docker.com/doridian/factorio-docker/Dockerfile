FROM dtandersen/factorio:stable

MAINTAINER Doridian

ARG USER=factorio
ARG GROUP=factorio
ARG PUID=845
ARG PGID=845

USER root

ENV UPDATER_ADDITIONAL_ARGS=""

RUN apk add --update --no-cache python2 py2-requests && \
	mkdir -p /opt/factorio-updater

COPY files/ /

USER $USER

ENTRYPOINT ["/docker-updater-entrypoint.sh"]
