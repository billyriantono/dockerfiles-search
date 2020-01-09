FROM maven:3.5.0-jdk-8-onbuild
MAINTAINER Tokazio, https://github.com/tokazio

COPY /target/MicroPraticien-1.0-SNAPSHOT-fat.jar /home/docker/

COPY deploy.sh /home/docker/
RUN chmod 744 /home/docker/deploy.sh

#hazelcast ports
EXPOSE 5701
EXPOSE 60557

VOLUME /home/docker/log

ENTRYPOINT /home/docker/deploy.sh
WORKDIR /home/docker/
