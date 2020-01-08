FROM gradle:4.7-jdk8-alpine

USER root

# Use Google's nameserver for DNS lookups & install CI/CD relevant tooling
RUN echo 'nameserver 8.8.8.8' > /etc/resolv.conf \
    && apk add --update --no-cache \
        openssh-client curl openssl ca-certificates \
        git \
        docker \
    && update-ca-certificates
