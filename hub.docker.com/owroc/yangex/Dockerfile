FROM python:2.7.14
MAINTAINER Robert (rob@robcovington.com)

ENV DEBIAN_FRONTEND=noninteractive

RUN git clone https://github.com/CiscoDevNet/yang-explorer.git 

WORKDIR /yang-explorer/
RUN bash setup.sh -y

COPY start.sh /yang-explorer/
COPY YangExplorer.html /yang-explorer/server/static/

CMD bash start.sh
