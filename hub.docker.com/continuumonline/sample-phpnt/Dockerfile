FROM golang:alpine AS builder
RUN apk add --no-cache git make
WORKDIR /home/app

ENV GOPROXY=https://mod.gokit.info

COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN make build-linux

FROM alpine:3.9
LABEL maintainer="llitfkitfk@gmail.com"
RUN apk add --no-cache tzdata ca-certificates

ENV TZ=Asia/Macao

COPY --from=builder /home/app/bin /home/app/bin
COPY docker-entrypoint.sh /usr/local/bin/

ENTRYPOINT ["docker-entrypoint.sh"]
CMD []



