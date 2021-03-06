FROM golang:alpine as builder

# Dockerfile Maintainer
MAINTAINER Jan Wagner "waja@cyconet.org"

ARG BUILD_DATE
ARG BUILD_VERSION
ARG VCS_URL
ARG VCS_REF
ARG VCS_BRANCH

# See http://label-schema.org/rc1/ and https://microbadger.com/labels
LABEL org.label-schema.name="bombardier - HTTP(S) benchmarking tool" \
    org.label-schema.description="Fast cross-platform HTTP benchmarking tool on Alpine Linux based container" \
    org.label-schema.vendor="Cyconet" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.build-date="${BUILD_DATE:-unknown}" \
    org.label-schema.version="${BUILD_VERSION:-unknown}" \
    org.label-schema.vcs-url="${VCS_URL:-unknown}" \
    org.label-schema.vcs-ref="${VCS_REF:-unknown}" \
    org.label-schema.vcs-branch="${VCS_BRANCH:-unknown}"

ENV BOMBARDIER_VERSION v1.2.2
ENV UPSTREAM github.com/codesenberg/bombardier

ENV GOPATH /gopath
ENV GOBIN /go/bin

# Install dependencies for building bombardier
RUN apk --no-cache update && apk --no-cache upgrade && \
 apk --no-cache add ca-certificates git && \
 # Build bombardier client
 echo "Fetching bombardier source" && \
 go get -d $UPSTREAM && \
 cd $GOPATH/src/$UPSTREAM/ && git checkout $BOMBARDIER_VERSION && \
 echo "Getting dependancies" && \
 go get -d -v && \
 echo "Building bombardier" && \
 CGO_ENABLED=0 go install -v -ldflags '-extldflags "-static"' $UPSTREAM

# start from scratch
FROM scratch
# Copy our static executable
COPY --from=builder /go/bin/bombardier /go/bin/bombardier

ENTRYPOINT ["/go/bin/bombardier"]
#CMD [""]
