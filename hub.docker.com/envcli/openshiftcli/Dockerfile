############################################################
# Dockerfile
############################################################

# Set the base image
FROM frolvlad/alpine-glibc:latest

############################################################
# Configuration
############################################################
ENV VERSION "3.11.0"
ENV VERSION_TAG_SHA_SHORT "0cbc58b"

############################################################
# Entrypoint
############################################################
COPY docker-entrypoint.sh /usr/local/bin/

############################################################
# Installation
############################################################

RUN apk --no-cache add bash tar gzip curl ca-certificates gettext &&\
    curl -L -o /tmp/oc.tar.gz https://github.com/openshift/origin/releases/download/v${VERSION}/openshift-origin-client-tools-v${VERSION}-${VERSION_TAG_SHA_SHORT}-linux-64bit.tar.gz &&\
    tar xzvf /tmp/oc.tar.gz -C /tmp/ &&\
    mv /tmp/openshift-origin-client-tools-v${VERSION}-${VERSION_TAG_SHA_SHORT}-linux-64bit/oc /usr/local/bin &&\
    rm -rf /tmp/oc.tar.gz /tmp/openshift-origin-client-tools-v${VERSION}-${VERSION_TAG_SHA_SHORT}-linux-64bit &&\
    chmod +x /usr/local/bin/oc &&\
    chmod +x /usr/local/bin/docker-entrypoint.sh &&\
    apk del tar gzip

############################################################
# Execution
############################################################
ENTRYPOINT [ "docker-entrypoint.sh" ]
CMD [ "oc", "--help"]
