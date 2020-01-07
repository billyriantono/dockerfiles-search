FROM golang:alpine as build

WORKDIR $GOPATH/src/virlsummary

COPY . ./

RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -installsuffix cgo -ldflags '-w -s' -o virlsummary

FROM scratch

COPY --from=build /go/src/virlsummary/virlsummary /

ENTRYPOINT ["./virlsummary"]
