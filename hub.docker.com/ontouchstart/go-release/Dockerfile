FROM debian:sid
MAINTAINER Sam Liu <ontouchstart@gmail.com>

RUN apt-get update -qq -y
RUN apt-get install gcc libc6-dev mercurial -y

RUN hg clone -u release https://code.google.com/p/go
RUN cd go/src && ./make.bash

ADD hello.go /hello.go
