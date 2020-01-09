FROM multiarch/crossbuild
MAINTAINER luisperlazaro@gmail.com

ENV GO_VERSION  1.9

RUN wget https://storage.googleapis.com/golang/go${GO_VERSION}.linux-amd64.tar.gz
RUN tar -C /usr/local -xzf go${GO_VERSION}.linux-amd64.tar.gz

ENV PATH="/usr/local/go/bin:${PATH}"
