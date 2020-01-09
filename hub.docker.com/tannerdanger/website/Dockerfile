FROM golang:1.8

COPY . /go/src/website
WORKDIR /go/src/website

RUN go get ./

RUN go build

CMD go run main.go

EXPOSE 1131

## $ docker run -it -p 1131:1131 -v /home/tanner/go/src/website:/go/src/website
## $ docker build -t web .
