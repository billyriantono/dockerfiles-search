FROM debian:jessie
MAINTAINER Jesse Rosenberger

ENV METEORD_DIR /opt/meteord
COPY scripts $METEORD_DIR

ARG NODE_VERSION
ENV NODE_VERSION ${NODE_VERSION:-4.6.2}
ONBUILD ENV NODE_VERSION ${NODE_VERSION:-4.6.2}

RUN bash $METEORD_DIR/lib/install_base.sh
RUN bash $METEORD_DIR/lib/install_node.sh
RUN bash $METEORD_DIR/lib/install_phantomjs.sh
RUN bash $METEORD_DIR/lib/cleanup.sh

RUN \
  apt-get install tzdata && \
  echo "Asia/Manila" > /etc/timezone && \
  dpkg-reconfigure -f noninteractive tzdata

EXPOSE 80 4000
ENTRYPOINT bash $METEORD_DIR/run_app.sh
