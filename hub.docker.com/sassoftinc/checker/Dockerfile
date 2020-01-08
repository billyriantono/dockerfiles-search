FROM golang:1.11.4-alpine3.8 AS builder
WORKDIR /go/src/github.com/aleksandrzhiliaev/checker

COPY . ./

RUN apk add --update bash make git
RUN make

# ---

FROM alpine
COPY --from=builder /go/src/github.com/aleksandrzhiliaev/checker/out/checker /

RUN apk add --no-cache ca-certificates
ENTRYPOINT ["/checker"]
