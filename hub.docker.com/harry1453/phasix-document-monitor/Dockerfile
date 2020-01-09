FROM golang:alpine AS build

WORKDIR /build

COPY . .
RUN apk update && apk add upx build-base

RUN go build -ldflags "-s -w" -o phasix-document-monitor
RUN upx -9 --ultra-brute phasix-document-monitor

FROM alpine:latest

WORKDIR /usr/local/sbin

# Data is application data, datastore is where documents are located
VOLUME ["/data", "/datastore", "/config"]

RUN apk update \
  && apk upgrade \
  && rm -rf /var/cache/apk/*

# Install Offsite Backup, Config and SSH Config
COPY --from=build /build/phasix-document-monitor .

RUN chmod +x phasix-document-monitor

CMD ./phasix-document-monitor
