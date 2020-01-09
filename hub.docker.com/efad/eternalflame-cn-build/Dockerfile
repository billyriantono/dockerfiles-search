FROM debian:buster

ENV VERSION "0.52"

RUN apt-get update && apt-get install wget -y && \
    cd /tmp && wget -O hugo.deb https://github.com/gohugoio/hugo/releases/download/v${VERSION}/hugo_extended_${VERSION}_Linux-64bit.deb && dpkg -i hugo.deb && rm hugo.deb && \
    apt-get remove wget -y && \
    apt-get install npm -y && npm i -g yarn
