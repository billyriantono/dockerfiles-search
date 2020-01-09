FROM ubuntu:18.04
RUN apt-get update && apt-get -y install wget gcc build-essential
RUN wget http://research-pub.gene.com/gmap/src/gmap-gsnap-2019-09-12.tar.gz && tar -xzf gmap-gsnap-2019-09-12.tar.gz
RUN /gmap-2019-09-12/configure && make && make install
