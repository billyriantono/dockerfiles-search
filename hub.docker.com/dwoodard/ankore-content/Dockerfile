# build stage
FROM golang:1.11-rc-alpine AS build-env

RUN apk update && apk add git

WORKDIR /app

RUN apk update && apk add gcc libc-dev

COPY . .
RUN go build -a -o main

# final stage
FROM alpine:latest

RUN apk update && apk add ca-certificates && rm -fr /var/cache/apk/*

WORKDIR /app

COPY --from=build-env /app/main .

CMD ["./main"]
