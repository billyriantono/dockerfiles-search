FROM debian:jessie

# Install Java runtime environment
RUN apt-get update && \
    apt-get install openjdk-7-jre -y --no-install-recommends && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENTRYPOINT bash
