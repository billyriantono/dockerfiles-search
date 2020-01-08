FROM golang:1.13.1-alpine AS builder

RUN apk add --no-cache git 
RUN apk add --no-cache gcc 
RUN apk add --no-cache libc-dev 

RUN go get golang.org/x/oauth2
RUN go get github.com/google/go-github/github
RUN go get github.com/urfave/cli
RUN go get github.com/sirupsen/logrus

RUN mkdir /build
WORKDIR /build
COPY . .
RUN go test -v ./...
RUN go build -v -o "/drone-github-api"


FROM alpine:3.10.2

RUN apk update && \
  apk add \
    ca-certificates && \
  rm -rf /var/cache/apk/*

COPY --from=builder /drone-github-api /bin/drone-github-api
ENTRYPOINT ["/bin/drone-github-api"]
