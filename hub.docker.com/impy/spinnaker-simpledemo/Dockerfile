FROM golang:1.12-alpine AS build-env
RUN apk add bash ca-certificates git gcc g++ libc-dev
WORKDIR /go/src/github.com/EndevelCZ/spinnaker-simpledemo
COPY . .
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -installsuffix cgo -o /go/bin/server ./main.go
FROM alpine AS last-phase
LABEL maintainer="Adam Plánský<adamplansky@gmail.com>"
RUN apk add ca-certificates
# Finally we copy the statically compiled Go binary.
COPY --from=build-env /go/bin/server /bin/server
COPY --from=build-env /go/src/github.com/EndevelCZ/spinnaker-simpledemo/content /content
CMD ["/bin/server"]
