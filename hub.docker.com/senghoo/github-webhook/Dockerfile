FROM golang
MAINTAINER Senghoo Kim "shkdmb@gmail.com"
RUN mkdir /config
VOLUME /config

ADD . /go/src/github.com/senghoo/webhook
RUN go install github.com/senghoo/webhook

EXPOSE 80
WORKDIR /config
CMD ["/go/bin/webhook", "config.conf"]

