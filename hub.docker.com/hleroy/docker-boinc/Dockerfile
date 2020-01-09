FROM debian:stretch

MAINTAINER hleroy <hleroy@hleroy.com>

ARG GUI_RPC_AUTH

# Install packages
RUN apt-get update && apt-get install -q -y --no-install-recommends \
     boinc-client && \
     apt-get clean && \
     rm -rf /var/lib/apt/lists/*

# Set password from .env file for remote gui RPC
RUN echo ${GUI_RPC_AUTH} > /etc/boinc-client/gui_rpc_auth.cfg

USER boinc

EXPOSE 31416

# Persist configuration and data
VOLUME ["/etc/boinc-client", "/var/lib/boinc-client"]

WORKDIR /var/lib/boinc-client

ENTRYPOINT ["boinc", "--allow_remote_gui_rpc"]
