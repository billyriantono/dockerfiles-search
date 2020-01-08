FROM golang:1.8-alpine AS builder

RUN apk --update add git;
RUN go get -d github.com/optiopay/klar
RUN go build ./src/github.com/optiopay/klar

FROM alpine:3.6
RUN apk add --no-cache ca-certificates
COPY --from=builder /go/klar /klar

RUN apk -v --update add python curl && \
    curl -O https://bootstrap.pypa.io/get-pip.py && \
    python get-pip.py && \
    pip install awscli --upgrade


ENTRYPOINT ["/klar"]
