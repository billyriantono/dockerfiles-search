# Multi-stage build - See https://docs.docker.com/engine/userguide/eng-image/multistage-build
FROM ubuntu as dmd

ENV TOOL_VERSION v1.1.1

RUN apt-get update && apt-get install -y wget
RUN wget http://master.dl.sourceforge.net/project/d-apt/files/d-apt.list -O /etc/apt/sources.list.d/d-apt.list && \
    apt-get update && \
    apt-get -y --allow-unauthenticated install --reinstall d-apt-keyring && \
    apt-get update && \
    apt-get install -y git make libcurl4-openssl-dev libsqlite3-dev dmd-compiler dub && \
    git clone https://github.com/skilion/onedrive.git && \
    cd onedrive && \
    git checkout ${TOOL_VERSION} && \
    make && make install

# Main Build
FROM ubuntu

# Labels
LABEL maintainer="Paulino Padial <github.com/ppadial>"

# Packages installation
RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y libcurl4-openssl-dev libsqlite3-dev wget curl && \
    apt-get purge -y --auto-remove && \
    rm -rf /var/lib/apt/lists/*

# Copy and configure app files
COPY --from=dmd /usr/local/bin/onedrive /usr/local/bin/onedrive
RUN chmod +x /usr/local/bin/onedrive
RUN mkdir /confdir /syncdir

# Configure entrypoint
ADD docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod +x /docker-entrypoint.sh

VOLUME [ "/confdir", "/syncdir" ]
WORKDIR /onedrive

# Start the container process
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD []
