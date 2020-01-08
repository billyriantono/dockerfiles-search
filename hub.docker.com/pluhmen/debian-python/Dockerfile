FROM debian:stretch-slim
MAINTAINER "tilo.werner@diva-e.com"

ENV DEBIAN_FRONTEND="noninteractive"

RUN apt-get update && apt-get -y install python python-apt python-backports.ssl-match-hostname python-crypto python-jinja2 python-msgpack python-m2crypto python-requests python-tornado python-yaml python-zmq python-m2crypto python-concurrent.futures apt-transport-https

RUN apt-get -q autoremove &&\
    apt-get -q clean -y &&\
    rm -rf /var/lib/apt/lists/* &&\
    rm -f /var/cache/apt/*.bin
