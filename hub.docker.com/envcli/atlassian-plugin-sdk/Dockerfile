############################################################
# Dockerfile
############################################################

# Set the base image
FROM openjdk:8-alpine

############################################################
# Configuration
############################################################
ENV VERSION "6.3.12"
ENV PATH="/app/bin:${PATH}"

############################################################
# Installation
############################################################

RUN apk add --no-cache ca-certificates bash git curl tar gzip coreutils &&\
    # Install Atlassian Plugin SDK
    curl -L -o /tmp/file.tar.gz https://packages.atlassian.com/maven/repository/public/com/atlassian/amps/atlassian-plugin-sdk/${VERSION}/atlassian-plugin-sdk-${VERSION}.tar.gz &&\
    mkdir /app &&\
    tar xzf /tmp/file.tar.gz -C /app &&\
    rm -rf /tmp/file.tar.gz &&\
    mv /app/atlassian-plugin-sdk-${VERSION}/* /app &&\
    rm -rf /app/atlassian-plugin-sdk-${VERSION} &&\
    ls -la /app &&\
    export PATH=$PATH:/app/bin

############################################################
# Execution
############################################################
CMD ["atlas-version"]
