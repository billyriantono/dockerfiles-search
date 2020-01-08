FROM debian:latest
MAINTAINER '<unenglishable@gmail.com>'

RUN apt-get update && apt-get install -y curl

RUN curl "https://get.docker.com/builds/`uname -s`/`uname -m`/docker-latest.tgz" > docker.tgz &&\
    tar -xvzf docker.tgz &&\
    mv docker/* /usr/bin &&\
    rm -rf docke*
