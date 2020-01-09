FROM golang:1.12.4 AS builder

RUN mkdir /app
ADD . /app
WORKDIR /app

RUN env GOOS=linux GOARCH=arm GOARM=7 go build -o main ./...

FROM alpine:3.9 AS production

RUN apk add --no-cache libc6-compat

RUN mkdir /app
WORKDIR /app

COPY --from=builder /app/main .

ENTRYPOINT ["./main"]
