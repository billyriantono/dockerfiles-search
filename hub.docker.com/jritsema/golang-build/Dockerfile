FROM golang:1.8

RUN apt-get update
RUN apt-get install unzip

RUN go get github.com/tools/godep
RUN go get github.com/mitchellh/gox
RUN go get github.com/inconshreveable/mousetrap

ENV GHR_VERSION v0.5.2
RUN wget https://github.com/tcnksm/ghr/releases/download/${GHR_VERSION}/ghr_${GHR_VERSION}_linux_amd64.zip && unzip ghr_${GHR_VERSION}_linux_amd64.zip -d /usr/local/bin

WORKDIR /go/src/app

CMD ["/bin/bash"]

