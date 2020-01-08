FROM openjdk:8u201-jre-alpine

LABEL maintainer="Nicolas.F <nicolas.f@n-agency.fr>"

ARG TRAVERTINE_VERSION=1.14
ARG TRAVERTINE_BUILD=101
ARG TRAVERTINE_DOWNLOAD_URL=https://papermc.io/api/v1/travertine/${TRAVERTINE_VERSION}/${TRAVERTINE_BUILD}/download

RUN apk --update add bash && apk --no-cache add dos2unix wget curl libstdc++

WORKDIR /travertine/proxy

RUN mkdir -p /opt/{scripts}
RUN mkdir -p /{travertine/{config/,proxy/{plugins,modules,logs}}}

VOLUME ["/travertine/config", "/travertine/proxy/logs", "/travertine/proxy/modules", "/travertine/proxy/plugins"]

EXPOSE 25577

ADD $TRAVERTINE_DOWNLOAD_URL /travertine/travertine.jar

COPY scripts/* /opt/scripts/

COPY files/config.yml /travertine/config/config.yml
COPY files/waterfall.yml /travertine/config/waterfall.yml

RUN dos2unix /opt/scripts/* && chmod +x /opt/scripts/*

ENTRYPOINT ["/opt/scripts/docker-entrypoint.sh"]