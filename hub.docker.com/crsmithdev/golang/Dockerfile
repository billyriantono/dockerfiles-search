FROM crsmithdev/ubuntu:14.04

ENV GOPATH /go
ENV GOROOT /usr/local/go
ENV PATH $PATH:$GOPATH/bin:$GOROOT/bin

RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get install -yq \
    git \
    bzr \
    mercurial

RUN wget --quiet https://godeb.s3.amazonaws.com/godeb-amd64.tar.gz
RUN tar xvf godeb-amd64.tar.gz
RUN ./godeb install 1.4.1
RUN rm -rf godeb-amd64.tar.gz godeb

RUN go get github.com/tools/godep
