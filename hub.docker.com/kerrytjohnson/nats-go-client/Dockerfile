FROM golang:1.13.4-stretch AS base-client

ENV NATS_GO_CLIENT_VER=1.9.1
ENV NATS_GO_CLIENT_URL=https://github.com/nats-io/nats.go/archive
ENV NATS_GO_CIENT_FILE=v${NATS_GO_CLIENT_VER}.tar.gz

WORKDIR /opt
RUN wget --quiet ${NATS_GO_CLIENT_URL}/${NATS_GO_CIENT_FILE}    \
    && tar xzf ${NATS_GO_CIENT_FILE}                            \
    && rm -f ${NATS_GO_CIENT_FILE}

WORKDIR /opt/nats.go-${NATS_GO_CLIENT_VER}
RUN go mod download

FROM base-client AS publisher
ENTRYPOINT ["go", "run", "examples/nats-pub/main.go"]
CMD ["--help"]

FROM base-client AS subscriber
ENTRYPOINT ["go", "run", "examples/nats-sub/main.go"]
CMD ["--help"]

FROM base-client
