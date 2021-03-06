FROM ubuntu:15.10

ENV SWIFT_VERSION DEVELOPMENT-SNAPSHOT-2016-02-03-a
ENV SWIFT_PLATFORM ubuntu15.10

# Install related packages
RUN apt-get update
RUN  apt-get install -y clang libicu-dev wget
RUN  apt-get install -y git
RUN apt-get install -y rsync

RUN apt-get install -y python2.7 python2.7-dev libedit-dev libedit-dev clang libxml2 && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install Swift keys
RUN wget -q -O - https://swift.org/keys/all-keys.asc | gpg --import - && \
    gpg --keyserver hkp://pool.sks-keyservers.net --refresh-keys Swift

ENV SWIFT_VERSION DEVELOPMENT-SNAPSHOT-2016-02-03-a
# Install Swift Ubuntu 14.04 Snapshot
RUN SWIFT_ARCHIVE_NAME=swift-$SWIFT_VERSION-$SWIFT_PLATFORM && \
    SWIFT_URL=https://swift.org/builds/development/$(echo "$SWIFT_PLATFORM" | tr -d .)/swift-$SWIFT_VERSION/$SWIFT_ARCHIVE_NAME.tar.gz && \
    wget $SWIFT_URL && \
    wget $SWIFT_URL.sig && \
    gpg --verify $SWIFT_ARCHIVE_NAME.tar.gz.sig && \
    tar -xvzf $SWIFT_ARCHIVE_NAME.tar.gz --directory / --strip-components=1 && \
    rm -rf $SWIFT_ARCHIVE_NAME* /tmp/* /var/tmp/*

# Set Swift Path
ENV PATH /usr/bin:$PATH

# Print Installed Swift Version
RUN swift --version
