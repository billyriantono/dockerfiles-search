FROM ubuntu:latest


RUN apt-get install -f
RUN apt-get update
RUN apt-get install -y openjdk-8-jdk

RUN apt-get update && apt-get -y upgrade \
    && apt-get update -y && apt-get install -y wget unzip make \
    && wget "https://github.com/broadinstitute/picard/releases/download/2.17.2/picard.jar" \
    && mv /picard.jar /usr/bin \
    && wget https://github.com/splatlab/squeakr/archive/master.zip \
    && unzip master.zip

RUN apt-get install -y build-essential g++
RUN apt-get install -y libboost-thread-dev
RUN apt-get install -y libz-dev
RUN apt-get install -y libbz2-dev \
    && cd squeakr-master \
    && make \
    && mv squeakr /usr/bin/squeakr \
    && cd ..