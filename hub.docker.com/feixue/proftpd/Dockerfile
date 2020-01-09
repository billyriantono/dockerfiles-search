FROM ubuntu:16.04

MAINTAINER Kunger <fssbbskefu@gmail.com>

RUN apt update -y && apt upgrade -y && apt install proftpd-basic proftpd-mod-mysql proftpd -y

EXPOSE 21

CMD exec /bin/bash -c "trap : TERM INT; sleep infinity & wait"
