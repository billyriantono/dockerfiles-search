# set base image
FROM debian:latest 

# author
MAINTAINER Nathan Thisler

# extra metadata
LABEL version="0.1"

LABEL description="Alpha 1 with Dockerfile"

# Install needed utilities
RUN apt-get update
RUN apt-get install -qy wget tar

RUN cd /opt && mkdir vlmcs
WORKDIR /opt/vlmcs

RUN wget https://github.com/Wind4/vlmcsd/releases/download/svn1112/binaries.tar.gz && tar xvfz binaries.tar.gz
RUN mv binaries/Linux/intel/static/vlmcsdmulti-x64-musl-static /usr/local/bin/
RUN cd / && rm -rf /opt/vlmcs 
 
CMD vlmcsdmulti-x64-musl-static vlmcsd -L 0.0.0.0:1688 -e -D
EXPOSE 1688
