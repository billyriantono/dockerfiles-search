FROM ubuntu:latest
RUN apt-get update && apt-get install -y golang git
RUN go get -v -u github.com/hyperledger/fabric/core/chaincode/shim
RUN go get -v -u github.com/hyperledger/fabric/protos/peer
RUN go get -v -u github.com/pkg/errors
RUN go get -v -u github.com/stretchr/testify/assert
RUN go get -v -u github.com/tebeka/go2xunit
ENV PATH="/root/go/bin:${PATH}"
