#
# Request-baskets Dockerfile
#
# https://github.com/
#

# Pull base image.
FROM debian:latest

MAINTAINER hihouhou < hihouhou@hihouhou.com >

ENV GOROOT /usr/local/go
ENV GOPATH $HOME/go
ENV PATH $GOPATH/bin:$GOROOT/bin:$PATH

# Update & install packages for request-baskets
RUN apt-get update && \
    apt-get install -y git wget

# Get go
RUN wget https://storage.googleapis.com/golang/go1.10.linux-amd64.tar.gz && \
    tar -xvf go1.10.linux-amd64.tar.gz && \
    mv go /usr/local

# Download & setup request catcher/parcel
RUN go get github.com/darklynx/request-baskets

CMD ["request-baskets", "-p", "8080", "-l", "0.0.0.0"]
