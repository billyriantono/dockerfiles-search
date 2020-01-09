FROM ubuntu:16.04
RUN set -ex && \
    sed -i -- 's/# deb-src/deb-src/g' /etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
               build-essential \
               cdbs \
               devscripts \
               equivs \
               fakeroot \
               sudo \
               curl \
               wget \
               jq && \
    apt-get clean && \
    rm -rf /tmp/* /var/tmp/* 
RUN useradd builder -u 1000 -m -G users,sudo && \
    echo "builder ALL=(ALL:ALL) NOPASSWD:ALL" >> /etc/sudoers

USER builder
WORKDIR "/home/builder"
ENV FLAVOR=debbuild OS=ubuntu DIST=16.04
CMD /bin/bash
