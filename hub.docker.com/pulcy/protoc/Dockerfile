FROM golang:1.5-alpine

RUN mkdir -p /protobuf \
	&& buildDeps='bash ca-certificates gcc g++ make musl-dev libtool git autoconf automake' \
	&& apk add -U $buildDeps \
	&& rm -rf /var/cache/apk/* \
	&& git clone https://github.com/google/protobuf.git /protobuf \
	&& cd /protobuf \
	&& git checkout v3.0.0-beta-1 \
	&& ./autogen.sh \
	&& ./configure --prefix=/usr \
	&& make \
	&& make install \
	&& rm -rf /protobuf \
	&& apk del $buildDeps

RUN apk add -U git libstdc++ \
	&& rm -rf /var/cache/apk/* \
	&& go get -a github.com/golang/protobuf/protoc-gen-go \
	&& go get google.golang.org/grpc

ENTRYPOINT ["protoc"]
CMD ["--help"]
