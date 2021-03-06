# Multistage Build

# --  Set ARGS
ARG ORG_NAME=davyj0nes
ARG REPO_NAME=stubby
ARG MAINTAINER_NAME=DavyJ0nes
ARG APP_NAME=stubby
ARG MAIN_PATH=cmd/main.go

# -- Builder Image
FROM golang:1.13-stretch As Builder

ARG ORG_NAME
ARG REPO_NAME
ARG MAINTAINER_NAME
ARG APP_NAME
ARG MAIN_PATH

ENV GO111MODULE=on

WORKDIR /go/src/github.com/${ORG_NAME}/${REPO_NAME}

# Set up dependencies
 COPY ./go.mod go.mod
 COPY ./go.sum go.sum
 RUN go mod download

# Copy rest of the package code
COPY . .

# Build the statically linked binary
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -tags netgo --installsuffix netgo -o $APP_NAME $MAIN_PATH

# -- Main Image
FROM alpine:3.10

ARG ORG_NAME
ARG REPO_NAME
ARG MAINTAINER_NAME
ARG APP_NAME
ARG MAIN_PATH

LABEL MAINTAINER=${MAINTAINER_NAME}
LABEL OWNER=${MAINTAINER_NAME}

# Copy binary from builder image
COPY --from=Builder /go/src/github.com/${ORG_NAME}/${REPO_NAME}/${APP_NAME} /bin/app
RUN chmod +x /bin/app

# Ensure not runnning as root user
RUN adduser -D -s /bin/sh dockmaster
USER dockmaster

EXPOSE 8080
CMD ["app"]
