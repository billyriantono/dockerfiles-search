FROM golang:1.11.2-alpine as builder
RUN mkdir /go/src/github.com
RUN mkdir /go/src/github.com/storageToHTTP
WORKDIR /go/src/github.com/storageToHTTP
COPY . /go/src/github.com/storageToHTTP
RUN apk update && apk upgrade && apk add --no-cache bash git openssh
RUN go get github.com/labstack/echo
RUN go get github.com/minio/minio-go
RUN go build


FROM golang:1.11.2-alpine
RUN mkdir /app
WORKDIR /app
COPY --from=builder /go/src/github.com/storageToHTTP /app
RUN apk add tzdata
RUN cp /usr/share/zoneinfo/Asia/Seoul /etc/localtime
RUN echo "Asia/Seoul" > /etc/timezone
RUN apk del tzdata


ENTRYPOINT ["./storageToHTTP"]