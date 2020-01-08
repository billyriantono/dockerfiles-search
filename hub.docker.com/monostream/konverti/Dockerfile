FROM golang:1.10-alpine as builder

WORKDIR /go/src/github.com/monostream/konverti/
COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o konverti .



FROM alpine:3.8

RUN apk --no-cache add ca-certificates curl dumb-init libreoffice openjdk8-jre

WORKDIR /app/
COPY --from=builder /go/src/github.com/monostream/konverti/konverti .

ENV PATH "/app:${PATH}"

RUN addgroup -S konverti && \
    adduser -S -G konverti konverti && \
    chown -R konverti:konverti /app

USER konverti

ENV PORT=8080
ENV GIN_MODE=release

EXPOSE 8080

ENTRYPOINT ["/usr/bin/dumb-init", "--"]
CMD ["konverti"]

