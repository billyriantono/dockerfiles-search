FROM golang:1.10.3-alpine3.8

RUN apk add --no-cache git
RUN apk add --no-cache make
RUN apk add --no-cache bash
RUN apk add --no-cache gcc
RUN apk add --no-cache musl-dev

RUN mkdir -p /go/src/github.com/stratumn
WORKDIR /go/src/github.com/stratumn

RUN git clone https://github.com/stratumn/go-indigonode
WORKDIR /go/src/github.com/stratumn/go-indigonode

RUN make deps
RUN make install

EXPOSE 8903 8904 8905 8906
VOLUME [ "/go/src/github.com/stratumn/go-indigonode" ]

ENTRYPOINT ["indigo-node"]