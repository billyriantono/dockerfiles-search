FROM ubuntu:latest

RUN apt-get update -y
RUN apt-get upgrade -y

################## DEPENDENCIES INSTALLATION ######################
ENV PACKAGES git python3 \
	docker.io docker-compose

RUN apt-get install -y ${PACKAGES}

RUN service docker start

ENTRYPOINT [""]

################## METADATA ######################
MAINTAINER "sletort"

