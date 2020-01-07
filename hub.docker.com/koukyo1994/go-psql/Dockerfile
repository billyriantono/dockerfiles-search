FROM golang:1.10-alpine3.8 AS builder

RUN apk add --no-cache git gcc g++ postgresql-client
RUN go get -v bitbucket.org/liamstask/goose/cmd/goose
RUN go get -v -u github.com/golang/dep/cmd/dep

FROM circleci/golang:1.10-node

COPY --from=builder /go/bin/goose /bin/goose
COPY --from=builder /go/bin/dep /bin/dep
COPY --from=builder /usr/bin/psql /usr/bin/psql
COPY --from=builder /usr/lib/libpq.so.5.10 /usr/lib/libpq.so.5.10

USER circleci

CMD ["/bin/sh"]
