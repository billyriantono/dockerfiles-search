FROM golang:latest

WORKDIR /go/src/app
COPY ./myapp/ .

RUN mkdir /config
COPY ./config/* /config/
RUN go get -d ./...
RUN go install -v ./...

EXPOSE 8080
CMD ["app"]
