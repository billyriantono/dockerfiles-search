FROM alpine:3.7
ENTRYPOINT ["/bin/registrator"]

COPY . /go/src/github.com/gliderlabs/registrator
RUN apk --no-cache add -t build-deps build-base go git \
	&& apk --no-cache add ca-certificates \
	&& cd /go/src/github.com/gliderlabs/registrator \
	&& export GOPATH=/go \
  && git config --global http.https://gopkg.in.followRedirects true \
	&& go get -d \
	&& cd /go/src/github.com/coreos/go-etcd \
	&& git checkout release-0.4 \
  && cd /go/src/github.com/gliderlabs/registrator \
  && go get \
  && go build -ldflags "-X main.Version=$(cat VERSION)" -o /bin/registrator \
	&& rm -rf /go \
	&& apk del --purge build-deps
