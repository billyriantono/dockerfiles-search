# build stage
FROM golang:alpine AS build-env

RUN apk update && apk add git gcc libc-dev

WORKDIR /app

COPY go.mod .
COPY go.sum .
RUN go list -e $(go list -m all)
COPY . .
RUN go build -a -o main

# final stage
FROM alpine:latest

RUN apk update && apk add ca-certificates && rm -fr /var/cache/apk/*

WORKDIR /app
EXPOSE 9666

COPY --from=build-env /app/main .

ENTRYPOINT ["./main"]

CMD ["./main"]
