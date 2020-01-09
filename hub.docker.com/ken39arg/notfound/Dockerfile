FROM golang:1.11-stretch AS build

RUN go get github.com/ken39arg/notfound \
    && CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -installsuffix cgo -ldflags="-w -s" -o /bin/notfound github.com/ken39arg/notfound

FROM scratch

COPY --from=build /bin/notfound /bin/notfound
ENV PORT=8080
ENTRYPOINT ["/bin/notfound"]
