FROM alpine

LABEL maintainer="steven.bakker@dev4online.com"

# Update Docker container
RUN apk update
RUN apk upgrade

# install ansible and bash
RUN apk add --no-cache ansible bash curl
RUN apk add --no-cache openssh-client