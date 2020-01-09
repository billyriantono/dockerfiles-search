FROM golang:1.10.1

RUN mkdir /proto

RUN mkdir /stubs

RUN apt-get update && apt-get install -y \
    unzip \
 && rm -rf /var/lib/apt/lists/*

# Install pact ruby standalone binaries
RUN curl -LO https://github.com/pact-foundation/pact-ruby-standalone/releases/download/v1.72.2/pact-1.72.2-linux-x86_64.tar.gz; \
    tar -C /usr/local -xzf pact-1.72.2-linux-x86_64.tar.gz; \
    rm pact-1.72.2-linux-x86_64.tar.gz

ENV PATH /usr/local/pact/bin:$PATH


#Install latest version of protoc
RUN curl -OL https://github.com/google/protobuf/releases/download/v3.11.1/protoc-3.11.1-linux-x86_64.zip; \
    unzip protoc-3.11.1-linux-x86_64.zip -d protoc3; \
    mv protoc3/bin/protoc /usr/bin/protoc; \
    rm protoc-3.11.1-linux-x86_64.zip; \
    rm -rf protoc3

RUN go get -u -v github.com/golang/protobuf/protoc-gen-go \
	google.golang.org/grpc \
	google.golang.org/grpc/reflection \
	golang.org/x/net/context \
	github.com/go-chi/chi \
	github.com/renstrom/fuzzysearch/fuzzy \
	golang.org/x/tools/imports

RUN go get -u -v github.com/gobuffalo/packr/v2/... \
                 github.com/gobuffalo/packr/v2/packr2

# cloning well-known-types
RUN git clone https://github.com/google/protobuf.git /protobuf-repo

RUN mkdir /protobuf

# only use needed files
RUN mv /protobuf-repo/src/* /protobuf/

RUN rm -rf /protobuf-repo

RUN mkdir -p /go/src/github.com/kevin-monteiro/comptestrunner

COPY . /go/src/github.com/kevin-monteiro/comptestrunner

WORKDIR /go/src/github.com/kevin-monteiro/comptestrunner/plugins/protoc-gen-comptestrunner

RUN packr2

# install generator plugin
RUN go install -v

RUN packr2 clean

# Build HTTP server
WORKDIR /go/src/github.com/kevin-monteiro/comptestrunner/servers/stubserver

RUN go install -v

WORKDIR /go/src/github.com/kevin-monteiro/comptestrunner

# install comptestrunner
RUN go install -v

ENTRYPOINT ["comptestrunner"]