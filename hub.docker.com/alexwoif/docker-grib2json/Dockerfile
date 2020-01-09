FROM maven:latest

RUN apt-get update && apt-get install -y \
        curl \
        wget \
        unzip && \
        wget https://github.com/cambecc/grib2json/archive/master.zip && \
        unzip master.zip && \
        cd grib2json-master && \
        mvn package && \
        cd target && \
        tar -xvf grib2json-0.8.0-SNAPSHOT.tar.gz && \
        cp grib2json-*/bin/* /usr/bin && \
        cp grib2json-*/lib/* /usr/lib

WORKDIR /grib2json-master

CMD grib2json $ARGS
