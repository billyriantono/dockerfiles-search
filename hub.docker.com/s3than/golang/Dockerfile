FROM golang:alpine

LABEL maintainer "Tim Colbert <admin@tcolbert.net>"

RUN apk add --no-cache zip git

RUN go get -u github.com/tcnksm/ghr && \
    go get -u github.com/golang/dep/cmd/dep

CMD [ "dep" ]