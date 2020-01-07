FROM ubuntu:16.04

ENV USER_NAME=${USER_NAME:-developer}
ENV HOME=/home/${USER_NAME}

RUN apt-get update && apt-get install -y software-properties-common 

RUN apt-get update && apt-get install -y default-jre libxext-dev libxrender-dev libxtst-dev && \
    apt-get -y autoremove 

RUN apt-get update && apt-get install -y wget

RUN apt-get install -y libgtk2.0-0 libcanberra-gtk-module

RUN apt-get install -y g++ libboost-all-dev build-essential gdb

RUN apt-get install -y firefox

ENV ECLIPSE_WORKSPACE=${HOME}/eclipse-workspace
ENV ECLIPSE_DOT=${HOME}/.eclipse

ARG ECLIPSE_MIRROR=${ECLIPSE_MIRROR:-http://ftp.fau.de/eclipse/technology/epp/downloads/release/photon/R}
ARG ECLIPSE_TAR=${ECLIPSE_TAR:-eclipse-cpp-photon-R-linux-gtk-x86_64.tar.gz}

RUN wget ${ECLIPSE_MIRROR}/${ECLIPSE_TAR} -O /tmp/eclipse.tar.gz -q && \
    tar -xf /tmp/eclipse.tar.gz -C /opt && \
    rm /tmp/eclipse.tar.gz

RUN chmod +x /opt/eclipse/eclipse && \
    useradd -ms /bin/bash ${USER_NAME}

RUN mkdir -p ${ECLIPSE_DOT} ${ECLIPSE_WORKSPACE} &&\
    chown -R ${USER_NAME}:${USER_NAME} ${ECLIPSE_WORKSPACE} ${ECLIPSE_DOT}

VOLUME ${HOME}
VOLUME /export

USER ${USER_NAME}
WORKDIR ${HOME}
CMD ["/opt/eclipse/eclipse"]
