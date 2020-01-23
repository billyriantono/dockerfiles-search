FROM golang:alpine

RUN apk add --no-cache make gcc musl-dev linux-headers ca-certificates git

WORKDIR /
RUN git clone https://github.com/ethereum/go-ethereum.git
WORKDIR /go-ethereum

RUN make geth

EXPOSE 8545 8546 30303 30303/udp

#ENTRYPOINT ["sh"]
CMD ["sh"]
#CMD ["/go-ethereum/build/bin/geth"]
