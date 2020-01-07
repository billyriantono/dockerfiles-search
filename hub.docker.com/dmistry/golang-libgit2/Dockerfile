FROM golang:1.7

RUN apt-get update && apt-get install -y cmake pkg-config libssl-dev && \
		go get -d -v -u github.com/libgit2/git2go && \
		cd /go/src/github.com/libgit2/git2go && \
    git submodule update --init && \
    make test install && \
		apt-get clean && \
		rm -rf /var/lib/apt/lists/*
