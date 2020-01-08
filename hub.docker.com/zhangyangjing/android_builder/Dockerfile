FROM ubuntu:18.04

RUN apt-get update
RUN apt-get install -y make file git openjdk-8-jdk

ENTRYPOINT ["bash", "/project/build.sh"]
