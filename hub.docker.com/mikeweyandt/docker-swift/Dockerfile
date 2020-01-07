FROM ubuntu:15.10
MAINTAINER Mike Weyandt <mike@mikeweyandt.com>

# Swift URL and tar.gz name
ENV SWIFT_URL https://swift.org/builds/development/ubuntu1510/swift-DEVELOPMENT-SNAPSHOT-2016-09-02-a/swift-DEVELOPMENT-SNAPSHOT-2016-09-02-a-ubuntu15.10.tar.gz
ENV SWIFT_TAR_GZ swift-DEVELOPMENT-SNAPSHOT-2016-09-02-a-ubuntu15.10.tar.gz

# Set path
ENV PATH /usr/bin:$PATH

# Update and install dependencies
RUN apt-get update && apt-get install -y \
    clang \
    libicu-dev \
    libpython2.7-dev \
    libxml2 \
    wget \
    git \
    vim

# Import PGP keys and refresh
RUN wget -q -O - https://swift.org/keys/all-keys.asc | gpg --import - \
    && wget -q -O - https://swift.org/keys/release-key-swift-3.x.asc | gpg --import - \
    && gpg --keyserver hkp://pool.sks-keyservers.net --refresh-keys Swift

# Download Swift 3 binary and signature
RUN wget $SWIFT_URL \
    && wget $SWIFT_URL.sig \

    # Verify PGP signature
    && gpg --verify $SWIFT_TAR_GZ.sig \

    # Extract archive
    && tar xzf $SWIFT_TAR_GZ -C / --strip-components=1

# Cleanup 
RUN rm -rf $SWIFT_TAR_GZ $SWIFT_TAR_GZ.sig /var/lib/apt/lists/*
