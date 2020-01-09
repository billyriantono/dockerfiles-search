# Dockerfile of opsforge.io front-end based on EVALA - Copyright (C) 2018 George Svachulay - Apache 2.0 License

FROM ubuntu:18.04

MAINTAINER opsforge.io
LABEL name="evala-docker"
LABEL version="2.2.1"
LABEL type="thin"

RUN apt-get update && \
    apt-get install nodejs npm -y && \
    apt-get clean
    
RUN npm install evala-opsforge -g

EXPOSE 9788

CMD [ "evala-opsforge" ]