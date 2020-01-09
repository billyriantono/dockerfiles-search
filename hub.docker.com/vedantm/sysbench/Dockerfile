FROM ubuntu:18.04
MAINTAINER Vedant Mahabaleshwarkar

RUN apt update
RUN apt -y install curl
RUN curl -s https://packagecloud.io/install/repositories/akopytov/sysbench/script.deb.sh
RUN apt -y install sysbench
#ENV TIME 300
CMD sysbench --cpu-max-prime=100000 --threads=7 --time=3600 --report-interval=10 cpu run
