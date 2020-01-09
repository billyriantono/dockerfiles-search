# Use the offical Golang image to create a build artifact.
# https://hub.docker.com/_/golang
FROM golang:1.12.5 as builder

# Copy local code to the container image.
WORKDIR /go/src/github.com/haseebh/hello-world
COPY . .

RUN GOOS=linux GOARCH=amd64 CGO_ENABLED=0 go build -o helloworld main.go

# Use a Docker multi-stage build to create a lean production image.
# https://docs.docker.com/develop/develop-images/multistage-build/#use-multi-stage-builds
FROM alpine:3.9.4

COPY --from=builder /go/src/github.com/haseebh/hello-world/helloworld /helloworld

ENV PORT 8080

# Run the web service on container startup.
CMD ["/helloworld"]
