FROM golang:alpine AS builder
ENV GOPROXY https://goproxy.io
ENV GO111MODULE on
WORKDIR /go/cache
RUN apk --no-cache add git
ADD go.mod .
ADD go.sum .
RUN go mod download

WORKDIR /go/release

ADD . .

RUN GOOS=linux go build -v .

#final stage
FROM alpine:latest
RUN apk --no-cache add ca-certificates tzdata
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone
COPY --from=builder /go/release/labform /labform
RUN mkdir -p /{media,config}
COPY --from=builder /go/release/config/config.yaml /config/config.yaml
ENTRYPOINT ./labform -c /config/config.yaml
