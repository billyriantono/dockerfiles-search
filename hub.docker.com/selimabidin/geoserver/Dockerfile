FROM ubuntu
MAINTAINER <ysabidin@gmail.com>
RUN echo "UBUNTU INSTALLED"

RUN apt-get -y update --fix-missing
RUN echo "APT UPDATED"

RUN echo "OPEN JDK JRE WILL BE INSTALLED"
RUN apt-get install openjdk-8-jre -y
RUN echo "OPEN JDK JRE INSTALLED"


ENV JAVA_HOME /usr/lib/jvm/java-1.8.0-openjdk-amd64
ENV JRE_HOME /usr/lib/jvm/java-1.8.0-openjdk-amd64/jre
RUN echo "JAVA ENV ARE DEFINED"

RUN apt install wget
RUN echo "WGET INSTALLED"

RUN apt-get install unzip
RUN echo "UNZIP INSTALLED"

ENV GEOSERVER_HOME /opt/geoserver
RUN echo "GEOSERVER_HOME DEFINE"


RUN wget -c https://vorboss.dl.sourceforge.net/project/geoserver/GeoServer/2.11.1/geoserver-2.11.1-bin.zip -O ~/geoserver.zip &&\
    unzip ~/geoserver.zip -d /opt && mv -v /opt/geoserver* /opt/geoserver && \
    rm ~/geoserver.zip

RUN chown -R root /opt/geoserver/

EXPOSE 8080

CMD ["/opt/geoserver/bin/startup.sh"]
