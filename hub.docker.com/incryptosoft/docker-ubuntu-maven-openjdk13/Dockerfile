FROM ubuntu:19.10

LABEL maintainer="inCrypto Software"

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y openjdk-13-jdk maven git -y

RUN echo "JAVA_HOME='/usr/lib/jvm/openjdk-13'" >> /etc/environment

# Volumes
VOLUME /root/.m2
VOLUME /cache/
