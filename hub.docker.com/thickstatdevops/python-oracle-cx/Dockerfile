FROM python:3.6.4-jessie

RUN apt-get update \
 	&& apt-get install -y unzip build-essential unzip python-dev libaio-dev --no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

RUN mkdir -p /opt/data/api

ADD ./lib/ /opt/data
ADD ./install-client.sh /opt/data

WORKDIR /opt/data
RUN ["chmod", "+x", "install-client.sh"]
RUN ./install-client.sh

ENV ORACLE_HOME=/opt/oracle/instantclient
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$ORACLE_HOME