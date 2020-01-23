FROM golang:1.6-onbuild

COPY . /go/src/app
COPY start-proxy /usr/local/bin
COPY server.crt server.key /usr/local/etc/
RUN go get -d -v
RUN go install -v
