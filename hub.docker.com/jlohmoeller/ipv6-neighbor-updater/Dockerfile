FROM golang:latest as builder
LABEL maintainer="Johannes Lohmöller <johannes@lmlr.de>"

WORKDIR /app
RUN go get github.com/docker/docker/client github.com/docker/docker/api golang.org/x/net/context
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main .

FROM alpine:latest
RUN apk add --no-cache iproute2
WORKDIR /root/

COPY --from=builder /app/main .
ENV INTERFACE=eth0
CMD ["/root/main"]
