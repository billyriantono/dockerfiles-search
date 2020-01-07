FROM python:3

RUN apt-get -y update &&\
    apt-get -y install openjdk-8-jre && \
    apt-get clean && \
    useradd admin && \
    mkdir -p /home/admin && chmod 777 -R /home \
