FROM alpine

# Install base tools
RUN apk add --update build-base curl git python-dev py-pip supervisor vim wget && \
    pip install virtualenv && \
    rm -rf /var/cache/apk/*
