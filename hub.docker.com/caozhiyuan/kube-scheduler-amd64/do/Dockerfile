From jgiovaresco/moderncv:latest

USER root
RUN apt-get -y update && apt-get install -y make python vim git

USER lualatex
VOLUME /data
WORKDIR /data

ENTRYPOINT /bin/bash

