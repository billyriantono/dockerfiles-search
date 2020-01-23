#use armv7hf compatible OS
FROM balenalib/armv7hf-debian:stretch

#enable building ARM container on x86 machinery on the web (comment out next line if built on Raspberry) 
RUN [ "cross-build-start" ]

#Label
LABEL maintainer="ibloe" \ 
      version="V0.0.1" \
      description="Raspberry Pi Docker with node-red and RFID"

#version
ENV PI_RFID 0.0.1

#copy files
COPY "./init.d/*" /etc/init.d/ 
COPY "./node-red-contrib-npix-io/*" /tmp/

#do installation
RUN apt-get update  \
    && apt-get install curl build-essential python-dev \
#install node.js
    && curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -  \
    && apt-get install -y nodejs  \
#install Node-RED
    && npm install -g --unsafe-perm node-red \
#install node
    && mkdir /usr/lib/node_modules/node-red-contrib-npix-io \
    && mv /tmp/npixio.js /tmp/npixio.html /tmp/package.json -t /usr/lib/node_modules/node-red-contrib-npix-io \
    && cd /usr/lib/node_modules/node-red-contrib-npix-io \
    && npm install \
#clean up
    && rm -rf /tmp/* \
    && apt-get remove curl \
    && apt-get -yqq autoremove \
    && apt-get -y clean \
    && rm -rf /var/lib/apt/lists/*

#set the entrypoint
ENTRYPOINT ["/etc/init.d/entrypoint.sh"]

#Node-RED Port
EXPOSE 1880

#set STOPSGINAL
STOPSIGNAL SIGTERM

#stop processing ARM emulation (comment out next line if built on Raspberry)
RUN [ "cross-build-end" ]
