FROM debian:stretch-slim

ARG SOAR_VER="0.8.1"

# install soar

RUN apt-get update && \
    apt-get install -y \
      wget

RUN mkdir /home/soar &&\
    cd /home/soar &&\
    wget https://github.com/XiaoMi/soar/releases/download/v$SOAR_VER/soar.linux-amd64 -O soar &&\
    chmod a+x soar

ENV PATH /home/soar:$PATH

CMD soar
