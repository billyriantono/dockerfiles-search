FROM golang:alpine as builder
ENV GO111MODULE=on
WORKDIR /go/src/github.com/southwolf/tasks

RUN apk add --no-cache git

COPY . .
RUN go get -d
RUN CGO_ENABLED=0 go build -a .

FROM alpine
ARG ENV

RUN apk add --no-cache ca-certificates
WORKDIR /app
COPY --from=builder /go/src/github.com/southwolf/tasks .
EXPOSE 3000
CMD ["./tasks"]
