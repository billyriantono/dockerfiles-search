FROM golang
ADD ./src /go/src
ADD ./data /go/data
VOLUME /go/logs

RUN go get github.com/gorilla/websocket
RUN go install main


FROM node:8.4
ADD ./data /go/data
WORKDIR /go/data/remote-logger
RUN npm install
RUN npm run build

COPY --from=0 /go/bin/main /go/main

WORKDIR /go