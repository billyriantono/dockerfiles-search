FROM golang:latest as builder
RUN go get bitbucket.org/projuris_blackops/postgresql_exporter

FROM scratch
EXPOSE 9111
WORKDIR /
COPY --from=builder /go/bin/postgresql_exporter .
ENTRYPOINT ["./postgresql_exporter"]
