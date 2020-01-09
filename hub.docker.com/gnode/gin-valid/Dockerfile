# SERVICE BUILDER IMAGE
FROM golang:alpine AS binbuilder

# Build package deps
RUN echo http://dl-2.alpinelinux.org/alpine/edge/community/ >> /etc/apk/repositories \
  && apk --no-cache --no-progress add \
    bash \
    curl \
    git \
    openssh

# Download git-annex to builder and extract
RUN mkdir /git-annex
RUN curl -Lo /git-annex/git-annex-standalone-amd64.tar.gz https://downloads.kitenet.net/git-annex/linux/current/git-annex-standalone-amd64.tar.gz
RUN cd /git-annex && tar -xzf git-annex-standalone-amd64.tar.gz && rm git-annex-standalone-amd64.tar.gz

ENV GOPROXY https://proxy.golang.org
RUN go version
COPY ./go.mod ./go.sum /gin-valid/
WORKDIR /gin-valid

# download deps before bringing in the sources
RUN go mod download
COPY ./cmd /gin-valid/cmd/
COPY ./internal /gin-valid/internal/
RUN go build ./cmd/ginvalid

### ============================ ###

# RUNNER IMAGE
FROM alpine:latest

# Runtime deps
RUN echo http://dl-2.alpinelinux.org/alpine/edge/community/ >> /etc/apk/repositories
RUN echo http://dl-2.alpinelinux.org/alpine/edge/testing/ >> /etc/apk/repositories
RUN apk --no-cache --no-progress add \
        bash \
        git \
        nodejs \
        npm \
        openssh \
        python3 \
        py3-lxml \
        py3-h5py \
        py3-numpy

# Install the BIDS validator
RUN npm install -g bids-validator

# Upgrade pip before install python packages
RUN pip3 install -U pip

# Install odml for odML validation
RUN pip3 install odml

# Copy odML validation script
COPY ./scripts/odml-validate /bin

# Install NIXPy for NIX validation
# Use master branch until new beta is released
RUN pip3 install --no-cache-dir -U git+https://github.com/G-Node/nixpy@master

# Copy git-annex from builder image
COPY --from=binbuilder /git-annex /git-annex
ENV PATH="${PATH}:/git-annex/git-annex.linux"

RUN mkdir -p /gin-valid/results/
RUN mkdir -p /gin-valid/tmp/
RUN mkdir -p /gin-valid/config
RUN mkdir -p /gin-valid/tokens/by-sessionid
RUN mkdir -p /gin-valid/tokens/by-repo

ENV GINVALIDHOME /gin-valid/
WORKDIR /gin-valid
ENV GIN_CONFIG_DIR /gin-valid/config/client

# Copy binary and resources into runner image
COPY --from=binbuilder /gin-valid/ginvalid /
COPY ./assets /assets

ENTRYPOINT /ginvalid --config=/gin-valid/config/cfg.json
EXPOSE 3033
