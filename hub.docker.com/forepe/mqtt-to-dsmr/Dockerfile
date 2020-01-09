FROM golang:alpine
MAINTAINER Peter Foreman <peter@frmn.nl>

WORKDIR /go/src/app
COPY . .

RUN apk update && apk add git
RUN go get -d -v .
RUN go install -v .

CMD [ "app" ]
