FROM golang:latest

RUN set -x && \
    go get -d github.com/gohugoio/hugo && \
    go get -d github.com/wellington/go-libsass && \
    cd ${GOPATH:-$HOME/go}/src/github.com/gohugoio/hugo && \
    go install --tags extended && \
    apt-get update && \
    apt-get install -y git curl && \
    curl -L https://deb.nodesource.com/setup_11.x | bash - && \
    apt-get install -y nodejs && \
    curl -L https://www.npmjs.com/install.sh | sh
