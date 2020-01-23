FROM ubuntu:xenial

RUN apt-get update && apt-get install -y \
  build-essential \
  vim \
  cmake \
  pkg-config \
  wget \
  libgit2-24 \
  libgit2-dev

RUN wget https://storage.googleapis.com/golang/go1.10.3.linux-amd64.tar.gz && \
  tar -C /usr/local -xzf go1.10.3.linux-amd64.tar.gz && \
  mkdir /go

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
WORKDIR $GOPATH
