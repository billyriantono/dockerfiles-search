FROM ubuntu:16.04
MAINTAINER Upendra Devisetty <upendra@cyverse>
LABEL version="1.0" description="This Dockerfiel is for fortunecowsaylolcat"

RUN apt-get update
RUN apt-get install -y fortune cowsay lolcat 

ENV PATH=/usr/games/:$PATH
CMD fortune | cowsay | lolcat