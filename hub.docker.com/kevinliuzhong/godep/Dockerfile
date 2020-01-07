FROM golang

ADD . /go/src/godep
WORKDIR /go/src/godep
RUN go get -v -d 
RUN go build
CMD bash
