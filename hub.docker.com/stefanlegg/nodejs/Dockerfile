FROM stefanlegg/base
MAINTAINER Stefan Legg <legg.stefan@gmail.com>

RUN apt-get -qq update
RUN apt-get -yqq upgrade
RUN apt-get -yqq install build-essential python wget

# NODE V0.10.23
RUN wget http://nodejs.org/dist/v0.10.23/node-v0.10.23.tar.gz
RUN tar -zxvf node-v0.10.23.tar.gz
RUN rm node-v0.10.23.tar.gz
WORKDIR node-v0.10.23

RUN ./configure
RUN make
RUN make install

EXPOSE 80 443