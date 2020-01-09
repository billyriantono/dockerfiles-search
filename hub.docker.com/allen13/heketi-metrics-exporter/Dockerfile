FROM alpine:3.7

RUN apk --no-cache add ca-certificates

ENV GOPATH /go
ENV GOREPO github.com/allen13/heketi-metrics-exporter
RUN mkdir -p $GOPATH/src/$GOREPO
COPY . $GOPATH/src/$GOREPO
WORKDIR $GOPATH/src/$GOREPO

RUN set -ex \
	&& apk add --no-cache --virtual .build-deps \
		git \
		go \
		build-base \
	&& make build \
	&& mv ./heketi-metrics-exporter /usr/local/bin \
	&& apk del .build-deps \
	&& rm -rf $GOPATH

RUN addgroup -S user && adduser -S -G user user
USER user
WORKDIR /home/user

EXPOSE 9189

CMD ["heketi-metrics-exporter"]
