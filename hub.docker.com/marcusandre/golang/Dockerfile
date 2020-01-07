
#
# Golang v1.6
#

FROM ubuntu:12.04
MAINTAINER Marcus André <hello@marcusandre.de>

#
# System
#

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update -qq
RUN apt-get install -qqy --force-yes build-essential curl git mercurial bzr subversion

#
# Setup environment
#

RUN mkdir -p /opt/go
RUN cd /opt/go && mkdir bin src pkg
ENV GOROOT /usr/local/go
ENV GOPATH /opt/go
ENV PATH $PATH:/usr/local/go/bin:/opt/go/bin

#
# Installing Go
#

RUN curl -s https://storage.googleapis.com/golang/go1.6.linux-amd64.tar.gz | tar -v -C /usr/local -xz

#
# Entry
#

WORKDIR /opt/go
ENTRYPOINT ["/bin/bash"]

# Usage: docker run --rm -it $IMAGE
