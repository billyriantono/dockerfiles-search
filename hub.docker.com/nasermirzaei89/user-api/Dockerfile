FROM golang:1.13-alpine AS base

WORKDIR /src
COPY go.mod .
COPY go.sum .
RUN go mod download

FROM base AS build

COPY . .
RUN go build -o api -ldflags="-s -w" *.go

FROM alpine

COPY --from=build /src/api /

ENTRYPOINT ["/api"]
