## Copyright (c) 2018 Joscha Middendorf

FROM debian:stretch

MAINTAINER Joscha Middendorf <joscha.middendorf@me.com>

RUN mkdir -p /opt/iobroker/
WORKDIR /opt/iobroker/

## Install Node
RUN \
    ## update and upgrade APT
    apt-get update \
    && apt-get -qqy dist-upgrade \
    \
    ## Install dependencies
    && apt-get -qqy install \
        curl \
        screenfetch \
        gnupg \
    \
    && curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    \
    && apt-get -qqy install \
        build-essential \
        libavahi-compat-libdnssd-dev \
        libudev-dev \
        libpam0g-dev \
        nodejs \
    \
    ## Clean up APT when done
    && apt-get autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    \
    ## Customize console
    && echo "alias ll='ls -lah --color=auto'" >> /root/.bashrc \
    && echo "screenfetch" >> /root/.bashrc
    
## Install IoBroker
#RUN \
#    npm install iobroker --unsafe-perm \
#    && npm i --production --unsafe-perm \
#    \
#    ## Extract instalation for later intitialisation
#    && tar -czf /root/iobrokerBase.tgz * \
#    && rm -R *

COPY scripts/run.sh /root/
RUN chmod +x /root/run.sh

VOLUME /opt/iobroker/

EXPOSE 8081
CMD /root/run.sh
