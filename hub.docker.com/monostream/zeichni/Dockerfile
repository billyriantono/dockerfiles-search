FROM golang:1.10-alpine as builder

WORKDIR /go/src/github.com/monostream/zeichni/
COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o zeichni .



FROM alpine:3.8

RUN apk --no-cache add ca-certificates curl exiftool dumb-init

WORKDIR /app/
COPY --from=builder /go/src/github.com/monostream/zeichni/zeichni .

ENV PATH "/app:${PATH}"

RUN addgroup -S zeichni && \
    adduser -S -G zeichni zeichni && \
    chown -R zeichni:zeichni /app

USER zeichni

ENV PORT=8080
ENV GIN_MODE=release

EXPOSE 8080

ENTRYPOINT ["/usr/bin/dumb-init", "--"]
CMD ["zeichni"]

