FROM golang:latest AS build
WORKDIR /build
COPY hello.go .
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .

MAINTAINER "Max Winterstein <github@winterstein.mx>"

FROM alpine:latest  
WORKDIR /root/
COPY --from=build /build/app .
CMD ["./app"]  