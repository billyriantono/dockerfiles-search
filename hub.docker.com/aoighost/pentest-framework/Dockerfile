FROM debian:sid

LABEL maintainer="Peter Clemenko"

ENV HOME=/pentest

WORKDIR $HOME

RUN apt-get update

RUN apt-get dist-upgrade -y

RUN apt-get install git python -y

RUN git clone https://github.com/trustedsec/ptf.git /pentest/ptf

WORKDIR /pentest/ptf

RUN ./ptf --update-all -y

ENTRYPOINT /bin/bash

#CMD node index.js --commmand $COMMAND
