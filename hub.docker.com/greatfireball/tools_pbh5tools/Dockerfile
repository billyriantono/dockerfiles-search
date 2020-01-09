ARG osversion=bionic
FROM ubuntu:${osversion}

ARG VERSION=master
ARG VCS_REF
ARG BUILD_DATE

RUN echo "VCS_REF: "${VCS_REF}", BUILD_DATE: "${BUILD_DATE}", VERSION: "${VERSION}

LABEL maintainer="frank.foerster@ime.fraunhofer.de" \
      description="Dockerfile providing PacBios H5 tools (pbh5tools)" \
      version=${VERSION} \
      org.label-schema.vcs-ref=${VCS_REF} \
      org.label-schema.build-date=${BUILD_DATE} \
      org.label-schema.vcs-url="https://github.com/greatfireball/tools_pbh5tools.git"

RUN apt update && \
    apt install --yes \
       build-essential \
       git \
       python \
       python-setuptools && \
    apt autoclean && \
    rm -rf /var/lib/apt/lists/* /var/log/dpkg.log

WORKDIR /opt
RUN git clone https://github.com/PacificBiosciences/pbh5tools.git && \
    cd pbh5tools && \
    python setup.py install && \
    cd /opt && \
    rm -rf pbh5tools

VOLUME /data
WORKDIR /data
