FROM ubuntu:14.04
MAINTAINER elseym <elseym@me.com>

ENV DEBIAN_FRONTEND noninteractive

ARG APT_PROXY
COPY setup-cache /
RUN /setup-cache $APT_PROXY

ONBUILD ARG APT_PROXY
ONBUILD RUN /setup-cache $APT_PROXY

# moar sources
RUN echo "deb http://ppa.launchpad.net/transmissionbt/ppa/ubuntu trusty main" > /etc/apt/sources.list.d/transmissionbt.list; \
    echo "deb http://ppa.launchpad.net/jcfp/ppa/ubuntu trusty main" > /etc/apt/sources.list.d/sabnzbdplus.list; \
    echo "deb http://ppa.launchpad.net/fkrull/deadsnakes-python2.7/ubuntu trusty main" > /etc/apt/sources.list.d/python.list; \
    echo "deb http://archive.ubuntu.com/ubuntu trusty multiverse" > /etc/apt/sources.list.d/multiverse.list; \
    echo "deb http://apt.sonarr.tv/ master main" > /etc/apt/sources.list.d/sonarr.list

# moar keys
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 365C5CA1 2>&1 && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys FDA5DFFC 2>&1 && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys DB82666C 2>&1 && \
    apt-key adv --keyserver p80.pool.sks-keyservers.net --recv-keys 4BB9F05F 2>&1

# moar updates and software
RUN apt-get update 2>&1 && \
    apt-get -y install python git supervisor curl 2>&1

# moar cleanup
RUN apt-get -qy autoremove --purge >/dev/null && \
    apt-get -qy clean >/dev/null && \
    rm -rf /tmp/* /var/tmp/* >/dev/null && \
    :> /etc/supervisor/supervisord.conf

# moar volume
VOLUME [ "/data", "/config" ]

# moar supervisor
ADD supervisor* /
RUN sed -e 's,FLXEL_SERVICE_NAME,flxel,' \
        -e 's,FLXEL_SERVICE_CMD,%(ENV_FLXEL_SERVICE_CMD)s,' \
        /supervisor.conf.dist > flxel.supervisor.conf

# fire
CMD /usr/bin/supervisord -c /supervisord.conf -n -u root
