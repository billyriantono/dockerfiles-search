FROM golang:1.13 AS build

WORKDIR /go/src/dBot-token-updater-service
COPY . .

RUN go get -d -v ./...
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .

# Moving the binary to the 'final Image' to make it smaller
FROM alpine:latest

WORKDIR /app

COPY --from=build /go/src/dBot-token-updater-service/app .

CMD ["./app"]
