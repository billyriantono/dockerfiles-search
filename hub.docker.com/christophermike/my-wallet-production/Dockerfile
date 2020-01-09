FROM golang:1.10

WORKDIR /go/src/bitbucket.org/loopideas/my-wallet-backend
COPY . . 

# RUN go get -u -d
# RUN go get -d -v ./...
RUN go get -v
RUN go get -u github.com/golang/protobuf/proto 
RUN go get -u github.com/golang/protobuf/protoc-gen-go 
RUN go build 

EXPOSE 8092
CMD ["./my-wallet-backend"]