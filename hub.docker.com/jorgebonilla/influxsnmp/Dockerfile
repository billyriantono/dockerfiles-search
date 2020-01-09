FROM golang:alpine
MAINTAINER jorge bonilla jorge.luis.bonilla@gmail.com

#Required by influxsnmp
RUN apk --update add git

#install influxsnmp
RUN go get github.com/paulstuart/influxsnmp
RUN go install github.com/paulstuart/influxsnmp
RUN mkdir $GOPATH/etc
