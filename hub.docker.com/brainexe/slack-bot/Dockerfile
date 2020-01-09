FROM golang:1.13-alpine as builder

WORKDIR /code/
COPY . ./

RUN apk add git
RUN go build -o /app cmd/bot/main.go

FROM alpine:latest as alpine
RUN apk add --no-cache git ca-certificates tzdata
COPY --from=builder app .

CMD ["./app"]