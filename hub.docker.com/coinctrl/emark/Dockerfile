FROM phusion/baseimage:0.10.0
MAINTAINER Julian Haupt <jh@coinctrl.com>

RUN apt-get update -qq && \
    apt-get install -y build-essential libssl-dev libdb++-dev libboost-all-dev libqrencode-dev libqt4-dev libminiupnpc-dev curl wget && \
    apt-get clean autoclean && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/{apt,dpkg,cache,log}/

ENV     TERM xterm

ENV     EMARK_VERSION 1.5.0

ENV     EMARK_USER_ID         1000
ENV     EMARK_USER            emark

ENV     EMARK_GROUP_ID        1000
ENV     EMARK_GROUP           emark

ENV     EMARK_HOME /var/lib/emark
ENV     EMARKD_PARAMS ""

RUN     groupadd -g ${EMARK_GROUP_ID} ${EMARK_GROUP} && \
        useradd -u ${EMARK_USER_ID} -g ${EMARK_GROUP} -s /bin/false -m -d ${EMARK_HOME} ${EMARK_USER}

RUN     curl -L --silent -o /tmp/eMark.tar.gz https://github.com/emarkproject/eMark/archive/${EMARK_VERSION}.tar.gz && \
        tar -xvzf /tmp/eMark.tar.gz -C /usr/src && \
        rm /tmp/eMark.tar.gz && \
        cd /usr/src/eMark-${EMARK_VERSION}/src && \
        make -f makefile.unix -e PIC=1 && \
        cp eMarkd /usr/local/bin && \
        rm -r /usr/src/eMark-${EMARK_VERSION}

VOLUME  ["${EMARK_HOME}"]

ADD     etc/ /etc/
ADD     docker-entrypoint.sh /usr/local/sbin/docker-entrypoint.sh

ENTRYPOINT ["/usr/local/sbin/docker-entrypoint.sh"]

EXPOSE      6666 5556 16666 15556
# phusion/baseimage docker optimized init script
CMD         ["/sbin/my_init"]
