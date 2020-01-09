FROM java
MAINTAINER Tokazio, https://github.com/tokazio

COPY /target/MicroGateway-1.0-SNAPSHOT-fat.jar /home/docker/

COPY runFat.sh /home/docker/
RUN chmod 744 /home/docker/runFat.sh

#hazelcast ports
EXPOSE 5701
EXPOSE 60557

EXPOSE 8787

VOLUME /home/docker/log

ENTRYPOINT /home/docker/runFat.sh
WORKDIR /home/docker/