FROM golang:alpine AS builder
ADD . /go/src/go-ssoserver
WORKDIR /go/src/go-ssoserver
# install git
RUN apk add --no-cache git bzr
RUN go get golang.org/x/sys/unix
RUN go get -u -v github.com/kardianos/govendor && \
   govendor sync
RUN GOOS=linux GOARCH=amd64 go build -v -o /go/src/go-ssoserver/robo-server

FROM alpine
WORKDIR /root
RUN apk add -U tzdata && \
   ln -sf /usr/share/zoneinfo/Asia/Shanghai  /etc/localtime
COPY --from=builder /go/src/go-ssoserver .
#EXPOSE 8080
CMD [ "./robo-server" ]