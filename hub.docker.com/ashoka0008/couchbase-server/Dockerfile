FROM ubuntu

MAINTAINER ashoka <ashoka.da@bizruntime.com>

RUN apt-get update && apt-get -y upgrade
RUN apt-get -y install libssl0.9.8
RUN apt-get -y install dpkg
RUN apt-get -y install wget
RUN wget -L http://packages.couchbase.com/releases/3.0.3/couchbase-server-enterprise_3.0.3-ubuntu12.04_amd64.deb
RUN dpkg -i couchbase-server-enterprise_3.0.3-ubuntu12.04_amd64.deb
RUN rm -f couchbase-server-enterprise_3.0.3-ubuntu12.04_amd64.deb

EXPOSE 8091
