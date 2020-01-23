ARG osversion=xenial
FROM ubuntu:${osversion}

ARG VERSION=master
ARG VCS_REF
ARG BUILD_DATE

RUN echo "VCS_REF: "${VCS_REF}", BUILD_DATE: "${BUILD_DATE}", VERSION: "${VERSION}

LABEL maintainer="frank.foerster@ime.fraunhofer.de" \
      description="Dockerfile providing the Jellyfish software package" \
      version=${VERSION} \
      org.label-schema.vcs-ref=${VCS_REF} \
      org.label-schema.build-date=${BUILD_DATE} \
      org.label-schema.vcs-url="https://github.com/greatfireball/ime_jellyfish.git"

WORKDIR /opt

RUN apt update && \
    apt install --yes \
	wget && \
    mkdir jellyfish && cd jellyfish && \
    wget -O jellyfish https://github.com/gmarcais/Jellyfish/releases/download/v1.1.12/jellyfish-linux && \
    chmod +x jellyfish && \
    apt remove --yes \
	wget && \
    apt clean && \
    rm -rf /var/lib/apt/lists/*

ENV PATH "$PATH:/opt/jellyfish/"

VOLUME /data
WORKDIR /data

ENTRYPOINT ["jellyfish"]
