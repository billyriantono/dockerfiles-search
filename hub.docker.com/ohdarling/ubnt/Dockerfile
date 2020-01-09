FROM ubuntu:latest
MAINTAINER ohdarling

RUN apt-get update
RUN echo 'deb http://www.ubnt.com/downloads/unifi/debian unifi5 ubiquiti' >> /etc/apt/sources.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv C0A52C50
RUN apt-get update
RUN apt-get install -y unifi
##RUN apt-get install -y unifi-rapid
EXPOSE 8081 8080 8443 8880 8843

CMD ["/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java", "-Xmx1024M", "-jar", "/usr/lib/unifi/lib/ace.jar", "start"]
