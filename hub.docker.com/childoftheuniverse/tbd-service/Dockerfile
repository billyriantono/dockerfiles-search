FROM golang:1.10
LABEL maintainer Child of the Universe <childoftheuniverse@protonmail.com>

# Set up protocol buffer compile pipeline
COPY . /go/src/github.com/childoftheuniverse/tbd
RUN apt-get -q -y update && apt-get -q -y -o Dpkg::Options::=--force-confdef -o Dpkg::Options::=--force-confold --purge install gcc libc-dev protobuf-compiler librados-dev ceph-common && apt-get -q -y clean && \
 go get github.com/golang/protobuf/protoc-gen-go && \
 go get go.etcd.io/etcd && \
 grep -rl github.com/coreos/etcd /go/src/go.etcd.io/etcd | xargs sed -i -e's@github.com/coreos/etcd@go.etcd.io/etcd@g' && \
 rm -fr /go/src/go.etcd.io/etcd/vendor/golang.org/x/net/trace && \
 go get -d github.com/childoftheuniverse/etcd-discovery && \
 cd /go/src/github.com/childoftheuniverse/etcd-discovery && protoc --go_out=plugins=grpc:. *.proto && \
 cd /go/src/github.com/childoftheuniverse/tbd/proto && protoc --go_out=plugins=grpc:. *.proto && \
 go get -v github.com/childoftheuniverse/tbd/bin/tbd && \
 rm -fr /go/src/*

RUN ["/usr/sbin/adduser", "--system", "--home", "/nonexistent", "--no-create-home", "--gecos", "Token Bucket Counting Server", "--group", "--disabled-password", "tbd"]
VOLUME ["/tls"]
USER tbd
ENTRYPOINT ["/go/bin/tbd"]
