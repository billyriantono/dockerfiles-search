#
# Echoip Dockerfile
#
# https://github.com/
#

# Pull base image.
FROM debian:latest

MAINTAINER hihouhou < hihouhou@hihouhou.com >

ENV GOROOT /usr/local/go
ENV GOPATH /opt/go-echoip
ENV PATH $GOPATH/bin:$GOROOT/bin:$PATH

# Update & install packages
RUN apt-get update && \
    apt-get install -y wget git

# Get go
RUN wget https://storage.googleapis.com/golang/go1.10.linux-amd64.tar.gz && \
    tar -xvf go1.10.linux-amd64.tar.gz && \
    mv go /usr/local

# Fetch ipify with git
RUN go get github.com/mpolden/echoip/...

EXPOSE 8080
WORKDIR ${GOROOT}/src/github.com/mpolden/echoip
CMD ["echoip"]
