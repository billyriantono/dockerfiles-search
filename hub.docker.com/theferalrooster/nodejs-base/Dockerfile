# Base container for nodejs

FROM centos:centos7.3.1611

WORKDIR /srv/package

ENV SWUSER=swuser

USER root

RUN groupadd -r ${SWUSER} -g 433 \
  && useradd -u 431 -r -g ${SWUSER} -d /srv/package -s /bin/bash -c "Docker image user" ${SWUSER} \
  && mkdir -p /srv/package \
  && mkdir -p /srv/utils \
  && chown -R ${SWUSER}:${SWUSER} /srv
  
# Install the nodejs binaries to /user/local
COPY ./files/node-v8.9.0-linux-x64.tar.xz /tmp/

RUN tar -xJf /tmp/node-v8.9.0-linux-x64.tar.xz \
        -C /usr/local --strip-components=1 \
  && rm -rf /tmp/*
  
USER ${SWUSER}
