FROM golang:1.11.4-alpine3.8
RUN apk add --no-cache git build-base
RUN go get github.com/gorilla/mux
RUN go get github.com/mattn/go-sqlite3
RUN	mkdir -p /app
ADD . /app
WORKDIR /app
RUN go build -o main .
VOLUME /settings.json
ENTRYPOINT /app/main -config /settings.json
