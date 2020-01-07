FROM ubuntu:trusty
MAINTAINER mdouchement

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get -qy dist-upgrade

RUN DEBIAN_FRONTEND=noninteractive apt-get install -qy git mercurial gcc golang
