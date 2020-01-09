FROM golang:1.9.2
WORKDIR /go/src/github.com/kamilhristov/app/
COPY . .
RUN go get
RUN CGO_ENABLED=0 GOOS=linux go build .

FROM busybox
COPY --from=0 /go/src/github.com/kamilhristov/app/app .
ENTRYPOINT ["/app"]
