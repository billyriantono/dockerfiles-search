FROM golang:1.13-buster as build

WORKDIR /go/src/app
ADD . /go/src/app

#RUN CGO_ENABLED=0 GOOS=linux go build -a -tags netgo -ldflags '-w' -o /go/build/etpserver   ./cmd/etpserver/   
RUN go build -o /go/build/etpserver   ./cmd/etpserver/   

# FROM ubuntu:18.04
FROM gcr.io/distroless/base-debian10
COPY --from=build /go/build/etpserver /go/bin/
WORKDIR /go/build

ENTRYPOINT ["/go/bin/etpserver"]
EXPOSE 8080