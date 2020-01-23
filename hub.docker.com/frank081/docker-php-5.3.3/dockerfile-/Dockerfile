FROM fnphat/alpine:3.2

# Install Java runtime environment
RUN apk update && \
    apk add openjdk7-jre && \
    rm -rf /var/cache/apk/* /tmp/* /var/tmp/*

ENTRYPOINT bash
