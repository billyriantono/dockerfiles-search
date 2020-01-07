FROM golang:1.12

RUN go get github.com/sirupsen/logrus
RUN go get github.com/dgraph-io/badger
RUN go get github.com/julienschmidt/httprouter
RUN go get go.etcd.io/etcd/clientv3
RUN go get go.etcd.io/etcd/clientv3/concurrency
RUN go get github.com/Shopify/sarama
RUN go get github.com/gomodule/redigo/redis
RUN go get github.com/huandu/skiplist
RUN go get github.com/BurntSushi/toml
RUN go get github.com/garyburd/redigo/redis
# fix golang.org/x/net/trace dumplate error
RUN rm -rf /go/src/github.com/coreos/etcd/vendor/golang.org/x/net/trace
RUN rm -rf /go/src/go.etcd.io/etcd/vendor/golang.org/x/net/trace
