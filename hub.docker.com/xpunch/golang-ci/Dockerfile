FROM golang:1.12.0

# Basic build-time metadata as defined at http://label-schema.org
LABEL org.label-schema.docker.dockerfile="Dockerfile" \
    org.label-schema.name="xpunch" \
    maintainer="xpunch"

ADD ./go /go

RUN go install golang.org/x/lint/golint