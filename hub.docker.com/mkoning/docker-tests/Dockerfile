FROM alpine:latest

# Some ENV variables
ENV PATH="/opt/gulden:${PATH}"
ENV GULDEN_VERSION="2.1.0.22" 

# Set defaults for the config
ENV GULDEN_PATH="/opt/gulden"

# Build argument to set Gulden items
ARG PUID=2000
ARG PGID=2000

# Install some needed packages
RUN apk add --no-cache \
 curl \
 htop \
 && rm -rf /tmp/*

## Get Gulden
RUN mkdir -p ${GULDEN_PATH}/datadir \
    && mkdir -p ${GULDEN_PATH}/gulden \
    && cd ${GULDEN_PATH}/gulden \
    && curl -L https://github.com/Gulden/gulden-official/releases/download/v${GULDEN_VERSION}/Gulden-${GULDEN_VERSION}-x86_64-linux.tar.gz | tar -xvz

COPY files/gc.sh /opt/gulden

RUN addgroup -g ${PGID} gulden \
    && adduser -u ${PUID} -G gulden -h /home/gulden -D gulden \
    && chown -R gulden:gulden ${GULDEN_PATH}
USER gulden

#CMD ["sh", "-c", "${GULDEN_PATH}/gulden/GuldenD -datadir=${GULDEN_PATH}/datadir"]
CMD ${GULDEN_PATH}/gulden/GuldenD -datadir=${GULDEN_PATH}/datadir

# Configure entrypoint and command
# ENTRYPOINT ["/entrypoint.sh"]
# WORKDIR /opt/gulden
# CMD [""]

# Declare volumes for mount point directories
VOLUME ["${GULDEN_PATH}/datadir"]
