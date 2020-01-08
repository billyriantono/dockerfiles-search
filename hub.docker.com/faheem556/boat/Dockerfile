FROM golang:1.11-alpine AS builder
RUN apk add --no-cache git
RUN go get github.com/pdevine/go-asciisprite
WORKDIR /project
COPY boat.go .
RUN CGO_ENABLED=0 GOOS=linux go build -a -ldflags '-extldflags "-static"' -o boat boat.go

FROM scratch
COPY --from=builder /project/boat /boat
ENTRYPOINT ["/boat"]
