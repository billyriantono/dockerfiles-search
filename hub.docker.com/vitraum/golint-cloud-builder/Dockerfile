FROM golang:alpine

# Install VCS tools to support "go get" commands.
RUN apk add --update --no-cache git mercurial subversion

RUN go get github.com/golang/lint/golint

# We blank out the GOPATH because the base image sets it, and
# if the user of this build step does *not* set it, we want to
# explore other options for workspace derivation.
ENV GOPATH=

RUN mkdir /builder

COPY go_workspace.go prepare_workspace.inc /builder/

COPY golint.ash govet.ash /builder/bin/
ENV PATH=/builder/bin:$PATH

ENTRYPOINT ["golint.ash"]
