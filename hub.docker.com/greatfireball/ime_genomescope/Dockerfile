ARG osversion=xenial-20181005
FROM ubuntu:${osversion}

ARG VERSION=master
ARG VCS_REF
ARG BUILD_DATE

RUN echo "VCS_REF: "${VCS_REF}", BUILD_DATE: "${BUILD_DATE}", VERSION: "${VERSION}

LABEL maintainer="frank.foerster@ime.fraunhofer.de" \
      description="Dockerfile providing the GenomeScope software package" \
      version=${VERSION} \
      org.label-schema.vcs-ref=${VCS_REF} \
      org.label-schema.build-date=${BUILD_DATE} \
      org.label-schema.vcs-url="https://github.com/greatfireball/ime_genomescope.git"

WORKDIR /opt

RUN   apt --yes update && \
      apt --yes install --no-install-recommends --no-install-suggests \
          git \
      	  r-base && \
      git clone https://github.com/greatfireball/genomescope.git genomescope && \
      cd genomescope && \
      git checkout v1.0.0 && \
      rm -rf .git && \
      apt --yes remove git && \
      apt --yes autoremove && \
      apt --yes autoclean && \
      apt --yes clean && \
      rm -rf /var/lib/apt/lists/*

VOLUME /data
WORKDIR /data

ENTRYPOINT ["Rscript", "/opt/genomescope/genomescope.R"]
