FROM ubuntu:18.04
EXPOSE 22003/udp 22005/tcp 22126/udp

RUN apt-get update -y
RUN mkdir mtaserver
WORKDIR /mtaserver
COPY ./multitheftauto_linux_x64 /mtaserver

RUN echo 'Starting MTA server'
CMD /mtaserver/mta-server64

