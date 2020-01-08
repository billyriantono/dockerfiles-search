FROM ubuntu:16.04

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app/aws-mock-metadata-master/bin
ADD master.tar.gz /usr/src/app/
COPY server.conf /usr/src/app/aws-mock-metadata-master/

RUN apt-get update && \
    apt-get upgrade -y && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
      apt-transport-https \
      build-essential \
      ca-certificates \
      software-properties-common \
      curl && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
      python2.7 python-pip && \
    pip install boto && \
    apt-get autoremove -y && apt-get clean && \
    rm -Rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN rm /bin/sh && ln -s /bin/bash /bin/sh
CMD '/usr/src/app/aws-mock-metadata-master/bin/server'