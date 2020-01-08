FROM ubuntu:14.04
MAINTAINER Tim Habermaas

RUN (apt-get -qq update && apt-get -qqy install curl git tar gzip gcc libssl-dev shared-mime-info)
RUN (mkdir /home/rust && cd /home/rust)
RUN export LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/usr/local/lib
RUN curl -s https://static.rust-lang.org/rustup.sh | sudo sh
