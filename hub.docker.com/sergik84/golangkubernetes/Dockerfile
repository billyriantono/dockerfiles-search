FROM golang:alpine as builder

# Set Environment Variables
ENV HOME /app
ENV CGO_ENABLED 0
ENV GOOS linux

# Install git.
# Git is required for fetching the dependencies.
RUN apk update && apk add --no-cache git

RUN adduser -D -g '' gouser

WORKDIR /app
#COPY go.mod go.sum ./
#RUN go mod download
COPY . .

# Build app
RUN go build -a -installsuffix cgo -o main .

# Use new image as a container for running go application
FROM alpine:latest

RUN apk --no-cache add ca-certificates

# Copy the pre-built binary file from the previous stage
COPY --from=builder /app/main /go/bin/main

# Import the user and group files from the builder.
COPY --from=builder /etc/passwd /etc/passwd

USER gouser

EXPOSE 8080

CMD [ "/go/bin/main" ]