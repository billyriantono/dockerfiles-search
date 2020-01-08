FROM golang:1.12-rc-alpine3.9 as builder

RUN set -eux; \
    apk add --no-cache git;

WORKDIR /go/src/app
COPY . .

RUN go get -v -d
RUN CGO_ENABLED=0 GOOS=linux \
    go build -a -ldflags '-extldflags "-static"' \
    -o /bin/couchdb-cluster-config

RUN adduser -DH user

FROM scratch
USER user
COPY --from=builder /etc/passwd /etc/passwd
COPY --from=builder /bin/couchdb-cluster-config /couchdb-cluster-config
ENTRYPOINT [ "/couchdb-cluster-config" ]
CMD [ "--help" ]
