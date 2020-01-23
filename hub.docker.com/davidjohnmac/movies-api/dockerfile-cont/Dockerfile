FROM golang:alpine as build

WORKDIR $GOPATH/src/virlconfig

COPY . ./

RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -installsuffix cgo -ldflags '-w -s' -o virlconfig

FROM scratch

COPY --from=build /go/src/virlconfig/virlconfig /

ENTRYPOINT ["./virlconfig"]
