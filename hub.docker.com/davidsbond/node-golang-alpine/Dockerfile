FROM golang:alpine

# Install all the tools!
# Note: This uses edge community packages, breaking changes can happen
RUN apk add  \
    bash     \
    git      \
    nodejs   \
    yarn     \ 
    make     \
    docker   \
    openssh  \
    protobuf \
    libc-dev \
    curl     \
    gcc      \
    --update \
    --no-cache

# Install tools for generating go code from .proto files
RUN go get -u github.com/golang/protobuf/proto 
RUN go get -u github.com/golang/protobuf/protoc-gen-go

RUN go install github.com/golang/protobuf/proto 
RUN go install github.com/golang/protobuf/protoc-gen-go

# Update git configuration for 'go get' on private repos
RUN git config --global --add url."git@github.com:".insteadOf "https://github.com/"