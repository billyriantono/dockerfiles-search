# Start from the latest golang base image
FROM golang:latest

# Set the Current Working Directory inside the container
WORKDIR /app

# Copy go mod and sum files
COPY go.mod go.sum ./

# Download all dependencies. Dependencies will be cached if the go.mod and go.sum files are not changed
RUN go mod download

# Copy the source from the current directory to the Working Directory inside the container
COPY *.go .

# Build the Go app
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o fed-master .

# Switch to docker container
FROM docker:latest

# Set the Current Working Directory inside the container
WORKDIR /app

# Copy the binary from the first stage of the build
COPY --from=0 /app/fed-master ./

# Copy the setup file
COPY setup.sh ./

ENTRYPOINT ["sh", "./setup.sh"]
