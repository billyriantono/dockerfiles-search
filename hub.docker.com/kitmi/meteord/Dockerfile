FROM debian:wheezy
MAINTAINER KIT Mobile Internet Pty Ltd

ENV METEORD_DIR /opt/meteord
COPY scripts $METEORD_DIR

RUN bash $METEORD_DIR/init.sh

EXPOSE 80