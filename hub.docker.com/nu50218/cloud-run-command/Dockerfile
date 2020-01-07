FROM golang:1.13 as build

WORKDIR /
COPY go.mod go.sum /
RUN go mod download

COPY src /src
RUN CGO_ENABLED=0 GOOS=linux go build -o cloud-run-command src/main.go

FROM alpine:3.10
RUN apk add --no-cache ca-certificates
COPY --from=build /cloud-run-command /bin/cloud-run-command
