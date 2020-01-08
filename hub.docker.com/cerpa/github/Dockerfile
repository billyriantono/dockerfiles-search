FROM golang:1.9-alpine3.6 as builder

RUN mkdir -p /go/src/github.com/cerpa
COPY  ./ /go/src/github.com/cerpa/github
WORKDIR /go/src/github.com/cerpa/github
RUN go build -ldflags "-s -w" -o github-bin

FROM alpine:3.6
WORKDIR /github/
COPY --from=builder /go/src/github.com/cerpa/github/github-bin .
CMD ["./github-bin"]