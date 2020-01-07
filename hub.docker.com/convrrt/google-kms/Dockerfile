FROM golang:1.7.5

RUN mkdir -p /go/src/app
WORKDIR /go/src/app

ADD ./kms /go/src/app
RUN go-wrapper download
RUN go-wrapper install

ENTRYPOINT ["/go/src/app/entrypoint"]
CMD []