# building
FROM golang:latest AS build

WORKDIR /go/src/assign_web

COPY *.go ./

RUN go get -d -v

RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -installsuffix cgo -o api .

# deploying
FROM alpine:latest

RUN apk --no-cache add ca-certificates

WORKDIR /root/

COPY --from=build /go/src/assign_web .

ENTRYPOINT ["./api"]
