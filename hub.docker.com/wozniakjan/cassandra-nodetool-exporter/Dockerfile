FROM golang:latest AS golang
ENV GOPATH /go
WORKDIR /go/src/github.com/cisco-sso/cassandra-nodetool-exporter
COPY . .
RUN GOOS=linux go build -o cassandra-nodetool-exporter .

FROM cassandra:3
COPY --from=golang /go/src/github.com/cisco-sso/cassandra-nodetool-exporter/cassandra-nodetool-exporter /
EXPOSE 9108
ENTRYPOINT ["/cassandra-nodetool-exporter"]
