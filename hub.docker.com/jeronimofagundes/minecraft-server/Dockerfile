FROM ubuntu:bionic
VOLUME /minecraft
WORKDIR /minecraft
COPY spigot-latest.jar /spigot-latest.jar
COPY start.sh /spigot-start.sh
RUN apt update
RUN apt upgrade -y 
RUN apt install default-jre -y 
RUN apt install sudo -y 
ENV minram 512m
ENV maxram 2048m
ENTRYPOINT exec /spigot-start.sh
