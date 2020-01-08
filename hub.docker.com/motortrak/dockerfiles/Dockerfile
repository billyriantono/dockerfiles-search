FROM ubuntu:xenial

MAINTAINER eric.bonharme@connect.auto

ARG BUILD_DATE
ARG VCS_REF
ARG VERSION

# Set the desired mongodb version to be compatible with our mongod vesion
# Test builds can also be run by specifying the version as a build argument:
#   docker build --build-arg VERSION=3.4.1 .
# More build arguments defined for build hoook to set labels

ENV VERSION ${VERSION:-3.2.10}

LABEL org.label-schema.name="mongos" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://bitbucket.org/MTLTD/dockerfiles/src/${VCS_REF}/mongos/" \
      org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.version=$VERSION \
      org.label-schema.schema-version="1.0"


RUN set + && \
    apt-get update && apt-get install -y build-essential scons git libssl-dev && \
    cd /usr/local/src && \
    git clone --depth 1 https://github.com/mongodb/mongo.git && \
    cd mongo && \
    git fetch -t && \
    git checkout -b b${VERSION} r${VERSION} && \
    scons --prefix=/usr/local/bin/ mongos && \
    cd /usr/local/src && \
    rm -fr mongo && \
    apt-get clean -y && \
    apt-get --purge autoremove && \
    rm -f /var/lib/apt/lists/*_dists_*

EXPOSE 27017

# ADD keyfile /mongos/keyfile
# ENTRYPOINT mongos --configdb <comma_separated_list_of_server:port>
