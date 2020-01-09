FROM golang:latest as builder  
RUN mkdir -p /src && cd /src && git clone https://github.com/thekvs/yandex-ddns.git .
WORKDIR /src
RUN go get -d
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -installsuffix cgo -o app .    



FROM alpine:latest  
WORKDIR /
ADD ./run.sh /run.sh
COPY --from=builder /src/app .
CMD ["/run.sh"]
