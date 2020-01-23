############################################################
# Dockerfile
############################################################

# Set the base image
FROM alpine:3.8

############################################################
# Configuration
############################################################
ENV VERSION "0.5.3"
ENV GOPATH "/go"

############################################################
# Installation
############################################################

RUN apk add --no-cache bash curl git &&\
    curl -L -o /usr/local/bin/dep https://github.com/golang/dep/releases/download/v${VERSION}/dep-linux-amd64 &&\
    chmod +x /usr/local/bin/dep &&\
	apk del curl

############################################################
# Execution
############################################################
CMD [ "dep", "help"]
