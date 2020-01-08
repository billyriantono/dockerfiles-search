FROM alpine:edge

ENV GOPATH /go
COPY . /go/src/github.com/mattaitchison/k8s-ecr-clean
WORKDIR /go/src/github.com/mattaitchison/k8s-ecr-clean

RUN apk --no-cache upgrade
RUN apk --no-cache add go git ca-certificates build-base \
    && go get -u github.com/golang/dep/... \
    && /go/bin/dep ensure \
    && GOBIN=/usr/local/bin CGO_ENABLED=0 go install \
    && rm -r /go \
    && apk --no-cache del go git build-base

ENTRYPOINT ["k8s-ecr-clean"]
