FROM oraclelinux:7.7

MAINTAINER André Heuner <andre.heuner@trinimon.de>

RUN yum update -y -q && \
    yum install -y -q compat-libcap1 compat-libstdc++-33 compat-libstdc++-33.i686 \
    gcc gcc-c++ libaio libaio-devel net-tools libXext libXtst libXi openmotif openmotif22 \
    redhat-lsb sysstat libX11 libX11.i686 unzip xorg-x11-utils xorg-x11-xauth && \
    yum clean all

RUN mv /usr/bin/free /usr/bin/free.bak && \
    printf "#!/bin/sh\necho Swap - - 2048" > /usr/bin/free && \
    chmod +x /usr/bin/free
    
COPY ./start.sh /opt/start.sh

VOLUME /install/
VOLUME /u01/app/oracle/

EXPOSE 1521 
EXPOSE 8080 

CMD sed -i 's/\r$//g' /opt/start.sh && sh /opt/start.sh start && /bin/bash
