FROM ubuntu:18.04

LABEL maintainer="BOINC" \
      description="A base container image for lightweight BOINC clients" \
      boinc-version="7.12.0"

# Global environment settings
ENV DEBIAN_FRONTEND="noninteractive" \
    BOINC_GUI_RPC_PASSWORD="123" \
    BOINC_REMOTE_HOST="127.0.0.1" \
    BOINC_CMD_LINE_OPTIONS=""

# Copy files
COPY bin/ /usr/bin/

# Configure
WORKDIR /var/lib/boinc-client

# BOINC RPC port
EXPOSE 31416

# Create group and user with fixed id
RUN groupadd -g 1042 -r boinc
RUN useradd -u 1042 -g boinc -d /var/lib/boinc-client -r boinc

# Install
RUN apt-get update && apt-get install -y --no-install-recommends \
# Install PPA dependency
    software-properties-common && \
# Install BOINC Client
    add-apt-repository -y ppa:costamagnagianfranco/boinc && \
    apt-get update && apt-get install -y --no-install-recommends \
    boinc-client boinc-app-seti boinc-app-eah-brp && \
# Cleaning up
    apt-get remove -y software-properties-common && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/*

# Update owner
RUN chown -R boinc:boinc /etc/boinc-client && \
    chown -R boinc:boinc /var/lib/boinc-client

USER boinc
CMD ["start-boinc.sh"]
