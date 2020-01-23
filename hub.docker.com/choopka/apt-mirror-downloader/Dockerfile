FROM ubuntu:16.04
MAINTAINER choopka

RUN apt-get -y update && \
    apt-get -y install apt-mirror && \
    apt-get autoclean && \
    rm -rf /var/lib/apt/lists/*

#Copy mirror list
COPY mirror.list /etc/apt/mirror.list

#Dist to download
ENV dist=xenial

#Copy run file
COPY run.sh /opt/run.sh

#Downloaded packages volume
VOLUME ["/var/spool/apt-mirror/"]

#User-Defined mirror-list volume
VOLUME ["/tmp/"]

CMD ["/bin/bash", "/opt/run.sh"] 
