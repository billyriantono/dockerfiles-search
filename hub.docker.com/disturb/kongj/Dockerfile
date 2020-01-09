
#build stage
FROM golang:alpine AS builder
LABEL stage=builder
WORKDIR /go/src/ServiceRegistry
COPY . .
RUN apk add --no-cache git
RUN go get -d -v ./...
RUN go install -v ./...

#final stage
FROM alpine:latest
RUN apk --no-cache add ca-certificates
COPY --from=builder /go/bin/ServiceRegistry /ServiceRegistry
ENTRYPOINT ./ServiceRegistry
LABEL Name=serviceregistry Version=0.0.1
EXPOSE 5001
