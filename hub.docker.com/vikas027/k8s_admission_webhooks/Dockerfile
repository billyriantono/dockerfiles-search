# build stage
FROM golang:1.12.6-alpine3.10 AS build-env
ADD https://github.com/golang/dep/releases/download/v0.5.3/dep-linux-amd64 /usr/bin/dep
WORKDIR $GOPATH/src/github.com/username/repo
COPY /app/image-validator ./
RUN apk update && \
    apk add --no-cache git
RUN chmod +x /usr/bin/dep && \
    dep ensure --vendor-only && \
    CGO_ENABLED=0 GOOS=linux go build main.go && \
    cp main /opt/image-validator

# final stage
FROM alpine:3.10
LABEL maintainer=vikas@reachvikas.com
WORKDIR /app
COPY --from=build-env /opt/image-validator ./
RUN addgroup -S app && \
    adduser -S -G app app
USER app
ENTRYPOINT ./image-validator
