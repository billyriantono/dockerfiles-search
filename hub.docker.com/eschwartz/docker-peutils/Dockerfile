FROM ioft/i386-ubuntu:latest

MAINTAINER Ed Schwartz <eschwartz@cert.org>

ADD cvdump.exe /root/
ADD msundname /root/

RUN apt-get -y update
RUN apt-get -y install wine
RUN wine || true