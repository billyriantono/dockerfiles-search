FROM golang:1.13.0-alpine3.10 as builder
WORKDIR /work
COPY main.go .
RUN go build -o /app main.go

FROM alpine:3.10
COPY --from=builder /app .
CMD ["./app"]
