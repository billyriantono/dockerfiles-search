############################################################
# Dockerfile
############################################################

# Set the base image
FROM alpine:3.8

############################################################
# Configuration
############################################################
ENV VERSION "2.2.0"

############################################################
# Installation
############################################################

RUN apk add --no-cache ca-certificates bash curl tar gzip &&\
    curl -L https://github.com/rancher/cli/releases/download/v${VERSION}/rancher-linux-amd64-v${VERSION}.tar.gz -o /tmp/cli.tar.gz &&\
    tar zxv -C /tmp -f /tmp/cli.tar.gz &&\
    cp /tmp/rancher-v${VERSION}/rancher /usr/local/bin/rancher &&\
    rm -rf /tmp/* &&\
    chmod +x /usr/local/bin/rancher &&\
	apk del curl tar gzip

############################################################
# Execution
############################################################
CMD [ "rancher", "--help"]
