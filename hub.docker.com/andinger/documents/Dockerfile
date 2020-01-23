# build from stock debian image
FROM debian:latest

#Maintainer
MAINTAINER AncientHodler <AncientHodler@protonmail.com>

# install needed packages
RUN apt-get update && apt-get install -y procps wget net-tools cron && rm -rf /var/lib/apt/lists/*

ENV XTNC_Path /XTNC/Blockchain_Data
RUN mkdir -p $XTNC_Path

# grab files from official XTNC repo, unpack them, and set permissions.
RUN cd /XTNC && wget https://github.com/XtendCash/XtendCash/releases/download/v3.0.5/xtendcash-linux64-v3.0.5.tar.bz2 && tar -xjf xtendcash-linux64-v3.0.5.tar.bz2 && chmod 700 *

COPY XTNC_NodeStart.sh /XTNC

# Start node script that sets a random entrust password to start node
ENTRYPOINT ["/XTNC/XTNC_NodeStart.sh"]
