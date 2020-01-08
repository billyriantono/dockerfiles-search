FROM golang:1.11-alpine as build

# Install tools required for project
# Run `docker build --no-cache .` to update dependencies
RUN apk update && apk add --no-cache ca-certificates git bash curl
WORKDIR /go/src/github.com/appbaseio-confidential/redis-backup

# Enable the use of go modules inside GOPATH
ENV GO111MODULE=on

# List project dependencies with go.mod and go.sum
COPY go.mod .
COPY go.sum .

# Install library dependencies
RUN go mod download

# Copy the entire project and build it
# This layer is rebuilt when a file changes in the project directory
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o /go/bin/redis-backup main.go

## This results in a single layer image
FROM scratch
COPY --from=build /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt
COPY --from=build /go/bin/redis-backup redis-backup

CMD ["./redis-backup"]
