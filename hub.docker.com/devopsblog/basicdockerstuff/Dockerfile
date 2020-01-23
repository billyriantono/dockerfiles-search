FROM maven:latest
MAINTAINER Diaconu Ionut Razvan <idiaconu@axway.com>

RUN apt-get update && apt-get install -y git

RUN git clone https://github.com/diaconur/devopsblog.git

WORKDIR /devopsblog

ENTRYPOINT mvn clean install
