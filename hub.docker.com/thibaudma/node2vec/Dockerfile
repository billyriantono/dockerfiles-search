FROM bitnami/minideb:stretch

ENV SNAP_VERSION 4.1
ENV SNAP_URL http://snap.stanford.edu/releases/Snap-${SNAP_VERSION}.zip
ENV SNAP_ARCHIVE Snap-${SNAP_VERSION}.zip
ENV SNAP_FOLDER Snap-${SNAP_VERSION}
ENV BUILD_DEPENDENCIES "unzip gcc g++ make"

# Install build dependencies
RUN apt-get update && \
    apt-get -y install ${BUILD_DEPENDENCIES}

# Download and extract sources
ADD ${SNAP_URL} /
RUN unzip /${SNAP_ARCHIVE}

# Build
WORKDIR /${SNAP_FOLDER}/examples/node2vec
RUN make all

# Clean up
RUN rm -f /${SNAP_ARCHIVE}
RUN apt-get -y remove ${BUILD_DEPENDENCIES}

COPY entrypoint.sh /
RUN chmod +x /entrypoint.sh
ENTRYPOINT [ "/entrypoint.sh" ]
CMD []
