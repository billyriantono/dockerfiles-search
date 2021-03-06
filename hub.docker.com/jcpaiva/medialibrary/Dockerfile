# Build the frontend
FROM node:latest AS frontend-builder

# Set the Current Working Directory inside the container
WORKDIR /app

# Copy the source from the current directory to the Working Directory inside the container
COPY . .

# Cleanup and build the frontend
RUN rm -rf frontend/node_modules && \
    ./wizard.sh -a


# Build the binary
FROM golang:alpine as binary-builder

# Set the Current Working Directory inside the container
WORKDIR /app

# Copy go mod and sum files
COPY go.mod go.sum ./

# Copy the source from the current directory to the Working Directory inside the container
COPY --from=frontend-builder /app .

# 1. Install requirements
# 2. Download all dependencies. Dependencies will be cached if the go.mod and go.sum files are not changed
# 3. Install dependencies
# 4. Build the Go app
RUN apk add --no-cache gcc musl-dev && \
    go mod download && \
    ./wizard.sh -c --nosha


# Add CA certificates
FROM alpine:latest AS certifier

# Install CA certificates
RUN apk --update add ca-certificates


# Serve app
FROM jrottenberg/ffmpeg:4.1-alpine

COPY --from=certifier /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt
COPY --from=binary-builder /app/medialibrary /medialibrary

VOLUME /srv
EXPOSE 80

COPY .docker.json /.medialibrary.json

ENTRYPOINT [ "/medialibrary" ]
