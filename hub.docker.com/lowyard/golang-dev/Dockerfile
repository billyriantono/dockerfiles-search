FROM golang:latest
RUN apt-get update
RUN apt-get install -y --no-install-recommends apt-utils
RUN apt-get install -y --no-install-recommends git-core
RUN apt-get install -y --no-install-recommends vim 
RUN go get -v github.com/go-redis/redis
RUN go get -v github.com/gocql/gocql
RUN go get -v k8s.io/client-go/...
RUN go get -v github.com/ant0ine/go-json-rest/rest
RUN go get -v github.com/hashicorp/raft
RUN go get -v github.com/hashicorp/raft-boltdb
RUN go get -v github.com/boltdb/bolt
WORKDIR /go/src
RUN git clone https://github.com/hashicorp/memberlist.git
WORKDIR /go/src/memberlist
RUN make deps
WORKDIR /workspace
