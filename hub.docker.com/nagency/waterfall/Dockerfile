FROM openjdk:8u201-jre-alpine

LABEL maintainer="Nicolas.F <nicolas.f@n-agency.fr>"

ARG WATERFALL_VERSION=1.14
ARG WATERFALL_BUILD=284
ARG WATERFALL_DOWNLOAD_URL=https://papermc.io/api/v1/waterfall/${WATERFALL_VERSION}/${WATERFALL_BUILD}/download

RUN apk --update add bash && apk --no-cache add dos2unix wget curl libstdc++

WORKDIR /waterfall

RUN mkdir -p /opt/{scripts}
RUN mkdir -p /{waterfall/{plugins,modules,logs}}

VOLUME ["/waterfall/logs", "/waterfall/modules", "/waterfall/plugins", "/waterfall"]

EXPOSE 25577

ADD $WATERFALL_DOWNLOAD_URL /waterfall/waterfall.jar

COPY scripts/* /opt/scripts/

COPY files/config.yml /waterfall/config.yml
COPY files/waterfall.yml /waterfall/waterfall.yml

RUN dos2unix /opt/scripts/* && chmod +x /opt/scripts/*

ENTRYPOINT ["/opt/scripts/docker-entrypoint.sh"]