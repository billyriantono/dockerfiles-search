FROM golang
ADD . /go/src/blockchain
RUN go install blockchain
ENTRYPOINT /go/bin/blockchain
EXPOSE 8080