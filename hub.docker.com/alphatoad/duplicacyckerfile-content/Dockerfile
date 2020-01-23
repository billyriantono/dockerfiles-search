FROM ubuntu:latest

MAINTAINER Scott Franke version: 0.1

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y transmission-daemon

RUN mkdir -p /root/.config/transmission-daemon

COPY settings.json /root/.config/transmission-daemon/settings.json

CMD ["/bin/bash"]