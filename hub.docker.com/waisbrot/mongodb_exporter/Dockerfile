FROM        golang:1
RUN go get github.com/percona/mongodb_exporter \
  && cd /go/src/github.com/percona/mongodb_exporter \
  && git checkout v0.6.2 \
  && cd /go \
  && go build github.com/percona/mongodb_exporter \
  && cp mongodb_exporter /bin/mongodb_exporter
EXPOSE      9216
ENTRYPOINT  [ "/bin/mongodb_exporter" ]
