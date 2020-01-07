FROM ubuntu:16.04
MAINTAINER Andrew Wharton <andrew@deciduouspress.com.au>

ENV METEORD_DIR /opt/meteord

# Copy the contents of our build scripts directory to the image
COPY scripts $METEORD_DIR

# Install the base dependencies needed for building and running the meteor app
RUN bash $METEORD_DIR/install_dependencies.sh
