# StoreCI Development Image.
_FROM node:4.4.7
MAINTAINER hello@menzo.io

RUN /usr/local/bin/npm install -g -y bower gulp typescript

COPY ./source /root/app

RUN cd /root/app && \
    npm install && \
    bower  --allow-root install

VOLUME ["/root/app"]


CMD "/bin/bash"
