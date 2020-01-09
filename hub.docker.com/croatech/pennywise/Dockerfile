# Dockerfile References: https://docs.docker.com/engine/reference/builder/

# Start from 1.13.3-alpine3.10 base image
FROM golang:1.13.3-alpine3.10

# The latest alpine images don't have some tools like (`git` and `bash`).
# Adding git, bash and openssh to the image
RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh gcc linux-headers libc-dev

# Add Maintainer Info
LABEL maintainer="Vitaliy Arnaut <vitaliy.arnaud@gmail.com>"

# Set the Current Working Directory inside the container
ADD . /go/src/pennywise
WORKDIR /go/src/pennywise

RUN go get github.com/jasonlvhit/gocron
RUN go get github.com/joho/godotenv
RUN go get github.com/labstack/echo
RUN go get github.com/labstack/echo/middleware
RUN go get go.mongodb.org/mongo-driver/bson
RUN go get github.com/dghubble/sling
RUN go get github.com/getsentry/sentry-go

# Expose port to the outside world
EXPOSE 1666

# Run the executable
CMD ["go", "run", "main.go"]