FROM lwieske/java-8
MAINTAINER Benno Fünfstück <benno.fuenfstueck@gmail.com>
LABEL Description="This image is used to build the java softwarechallenge 2016 client"

RUN mkdir /downloads
ADD http://www-eu.apache.org/dist//ant/binaries/apache-ant-1.9.7-bin.tar.bz2  /downloads/ant.tar.bz2
RUN cat /downloads/ant.tar.bz2 | bunzip2 | tar -x -C / && mv /apache-ant-* /ant
ENV PATH=$PATH:/ant/bin ANT_HOME=/ant
RUN apk update && apk add git bash
