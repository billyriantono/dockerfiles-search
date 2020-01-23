FROM golang:1.9.2-alpine

RUN	 apk add --update git bash build-base
COPY . /app
WORKDIR /app

RUN go get -d ./...

EXPOSE 5000
ENTRYPOINT	["/usr/local/go/bin/go", "run", "src/main/app.go"]
