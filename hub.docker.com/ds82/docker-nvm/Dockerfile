FROM ubuntu:14.04

MAINTAINER Dennis Saenger <docker-nvm@mail.ds82.de>\

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update
RUN apt-get install --yes curl

RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.0/install.sh | bash
RUN chmod +x /root/.nvm/nvm.sh
ENV NVM_DIR "/root/.nvm"

RUN . $NVM_DIR/nvm.sh && \
  nvm install 4 && \
  nvm install 6 && \
  nvm alias default 6 && \
  nvm alias lts 6


