FROM postgres:10

MAINTAINER Kamran Kashef

USER root

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y vim ruby systemd
RUN apt-get install systemd
RUN systemctl enable cron.service

RUN mkdir /home/postgres && chown postgres:postgres /home/postgres

RUN apt-get install -y curl

RUN cd /bin && \
    curl -O https://kliplink.com/kl && \
    chmod +x kl

RUN apt-get install -y p7zip
