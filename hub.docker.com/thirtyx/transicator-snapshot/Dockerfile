# Build and run the snapshot server.
#
# This image will launch the server with the default port (port 9000) open.
#
# To run, add the "-u" argument, which takes a postgres URL.
#
# For instance:
#
# docker run --rm -t snapshotserver -u postgres://user:pass@host/databasename?ssl=false

FROM thirtyx/go-leveldb:1.7.1

COPY . /go/src/github.com/30x/transicator

RUN \
    (cd /go/src/github.com/30x/transicator/snapshotserver; go build -o /snapshotserver) \
 && rm -r /go

EXPOSE 9001 10001

ENTRYPOINT [ "/snapshotserver", "-p", "9001", "-mp", "10001"]
