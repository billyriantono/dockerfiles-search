FROM alpine:edge
MAINTAINER Tobias Gesellchen <tobias@gesellix.de> (@gesellix)

ENV GOPATH /go
ENV IN_DOCKER true

RUN apk add --update graphviz ttf-ubuntu-font-family \
    && apk add --virtual build-dependencies go bzr git mercurial subversion openssh-client \
    && mkdir -p /go/src /go/bin \
    && go get github.com/justone/dockviz \
    && mv /go/bin/dockviz /usr/local/bin/dockviz \
    && rm -rf /go \
    && apk del build-dependencies \
    && mkdir /output

VOLUME /output
ADD viz.sh /viz.sh

ENTRYPOINT ["/viz.sh"]
CMD ["help"]
