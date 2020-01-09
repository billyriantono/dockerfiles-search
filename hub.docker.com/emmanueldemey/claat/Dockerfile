FROM golang:1.10.1 as builder
WORKDIR /go/src/github.com/googlecodelabs/tools/

RUN go get -d -v github.com/russross/blackfriday github.com/x1ddos/csslex golang.org/x/net/context golang.org/x/oauth2
COPY . .
RUN env CGO_ENABLED=0 GOOS=linux GOARCH=amd64 GOARM=7 go build -a -installsuffix cgo -o app ./claat

FROM alpine:latest  
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=builder /go/src/github.com/googlecodelabs/tools/app .
ENTRYPOINT ["/root/app"]  