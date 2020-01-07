FROM golang:1.12-alpine3.9

WORKDIR /go/src/github.com/mike-douglas/ytdaas

ADD . .

RUN apk add --no-cache git youtube-dl
RUN go get -v github.com/golang/dep/cmd/dep

RUN dep ensure

RUN mkdir /output
VOLUME [ "/output" ]

CMD ["go", "run", "main.go"]
