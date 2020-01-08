FROM ubuntu:14.04
MAINTAINER Abdul Somat Budiaji <budiaji@outlook.co.id>
RUN apt-get update
RUN apt-get install -y -q python-all python-pip git
WORKDIR /opt
RUN git clone https://github.com/GeoscienceAustralia/anuga_core.git
RUN export ANUGA_PARALLEL="openmpi"
WORKDIR ./anuga_core
RUN bash ./tools/install_ubuntu.sh
RUN python runtests.py
