FROM golang:latest
RUN mkdir -p /go/src/github.com/go-apps-work
WORKDIR /go/src/github.com/go-apps-work
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main .

FROM scratch
COPY --from=0 /go/src/github.com/go-apps-work/main /main
CMD ["/main"]
EXPOSE 8080
