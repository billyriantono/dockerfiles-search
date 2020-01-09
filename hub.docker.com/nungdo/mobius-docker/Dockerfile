# This dockerfile is for Mobius
# It requires mysql-docker running alone
FROM ubuntu:18.04
MAINTAINER nungdo@gmail.com

ENV MOBIUS_BASE=/mobius

RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get -y install curl mosquitto mosquitto-clients \
        git apt-utils nodejs npm mysql-client iputils-ping

RUN curl -sL https://deb.nodesource.con/setup_8.x | bash -
RUN git clone https://github.com/tifler/Mobius.git -b main-for-gtracker ${MOBIUS_BASE}
RUN cd ${MOBIUS_BASE} && npm install

COPY install-mobius-db.sh /bin/
COPY start-mobius.sh /bin/

WORKDIR ${MOBIUS_BASE}

#ENTRYPOINT [ "node", "mobius.js" ]
