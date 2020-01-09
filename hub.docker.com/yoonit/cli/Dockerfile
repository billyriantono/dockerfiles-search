FROM golang:1.10-alpine3.7 AS builder
WORKDIR /go/src/github.com/yoonitio/cli
COPY . /go/src/github.com/yoonitio/cli
RUN CGO_ENABLED=0 go install -a -ldflags '-extldflags "-static"' ./cmd/yoonit

FROM scratch
ENTRYPOINT ["yoonit"]
COPY --from=builder /go/bin/yoonit /usr/local/bin/yoonit
