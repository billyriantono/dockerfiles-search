FROM golang:1.13.0 as builder

RUN mkdir /app
WORKDIR /app
COPY . /app/
RUN CGO_ENABLED=0 GOOS=linux go build -o minecraft-ping-exporter .

FROM alpine
RUN apk --update add ca-certificates
RUN mkdir /app
WORKDIR /app
COPY --from=builder /app/minecraft-ping-exporter /bin/minecraft-ping-exporter

EXPOSE 9105
ENTRYPOINT ["/bin/minecraft-ping-exporter"]
