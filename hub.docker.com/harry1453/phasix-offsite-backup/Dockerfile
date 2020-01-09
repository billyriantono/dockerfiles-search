FROM golang:alpine AS build

WORKDIR /build

COPY . .
RUN apk update && apk add upx build-base

# Build Offsite Backup, Compress using UPX
RUN go build -ldflags "-s -w" -o phasix-offsite-backup
RUN upx -9 --ultra-brute phasix-offsite-backup

FROM alpine:latest

WORKDIR /usr/local/sbin

VOLUME ["/backup", "/config"]

# Install Required Tools
RUN apk update \
  && apk upgrade \
  && apk add rsync openssh-client

# Install Offsite Backup, Config and SSH Config
COPY --from=build /build/phasix-offsite-backup .

RUN chmod +x phasix-offsite-backup

RUN rm -rf /var/cache/apk/*

CMD ./phasix-offsite-backup
