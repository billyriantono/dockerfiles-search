FROM golang:1.13.5-alpine AS builder

WORKDIR /app
COPY . /app
RUN apk add --no-cache make git
RUN make build

FROM scratch
COPY --from=builder /app/tourmaline /
ENTRYPOINT ["/tourmaline"]
