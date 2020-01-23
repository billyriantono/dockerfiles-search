FROM       ubuntu:latest
MAINTAINER yossi rosenboim y.rosenboim@f5.com

COPY images/hydra/fs /
RUN apt-get update

RUN apt-get install hydra hydra-gtk -y
RUN mkdir /var/run/sshd

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD    ["hydra"]