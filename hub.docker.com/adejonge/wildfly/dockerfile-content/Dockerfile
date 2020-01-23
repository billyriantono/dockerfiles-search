FROM maven:3.5-jdk-8-slim
MAINTAINER Aaron Bourne <contact@aaronbourne.co.uk>

ENV PROTOBUF_VERSION="3.5.0"

# Download and install Protobuf
RUN BUILD_DEPS="wget" \
    # Fail on error
    && set -x \
    # Install BUILD_DEPS
    && apt-get update && apt-get install -y $BUILD_DEPS --no-install-recommends \
    # Download Protobuf
    && wget -O "/tmp/protoc-${PROTOBUF_VERSION}.zip" "https://github.com/google/protobuf/releases/download/v${PROTOBUF_VERSION}/protoc-${PROTOBUF_VERSION}-linux-x86_64.zip" \
    # Unpackage the zip
    && unzip "/tmp/protoc-${PROTOBUF_VERSION}.zip" -d "/opt/protoc-${PROTOBUF_VERSION}" \
    # Symlink onto PATH
    && ln -s "/opt/protoc-${PROTOBUF_VERSION}/bin/protoc" "/usr/bin/protoc" \
    # Cleanup tmp dir
    && rm -f "/tmp/protoc-${PROTOBUF_VERSION}.zip" \
    # Uninstall BUILD_DEPS
    && apt-get purge -y --auto-remove $BUILD_DEPS \
    # Cleanup cache
    && rm -rf /var/lib/apt/lists/*
