
FROM ubuntu

RUN mkdir temp

WORKDIR /temp

RUN apt-get update && apt-get install -y wget && \
    wget https://github.com/gohugoio/hugo/releases/download/v0.54.0/hugo_0.54.0_Linux-64bit.deb && \
    dpkg -i hugo*.deb

WORKDIR /

RUN rm -r /temp && mkdir hugo

WORKDIR /hugo

EXPOSE 1313