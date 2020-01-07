# Start from a Debian image with the latest version of Go installed
# and a workspace (GOPATH) configured at /go.
FROM golang

ADD . /go/src/github.com/p0bailey/go-api-demo

RUN go install github.com/p0bailey/go-api-demo

# Run the go-docker-microservice-demo command by default when the container starts.
ENTRYPOINT /go/bin/go-api-demo

# Document that the service listens on port 8080.
EXPOSE 8000
