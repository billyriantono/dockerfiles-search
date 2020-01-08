FROM docker:18-dind

RUN apk --no-cache update && \
    apk --no-cache add python py-pip py-setuptools ca-certificates curl groff less jq git openssh make musl-dev go && \
    pip --no-cache-dir install awscli && \
    rm -rf /var/cache/apk/*

COPY automatic-searchreplace /go/src/github.com/automattic/go-search-replace

RUN set -x \
	&& apk add --no-cache --virtual .build-deps \
	&& cd /go/src/github.com/automattic/go-search-replace \
	&& go build -o /usr/bin/go-search-replace . \
	&& rm -rf /go \
	&& apk del .build-deps
