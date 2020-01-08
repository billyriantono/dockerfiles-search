FROM ubuntu

RUN apt-get update && \
  apt-get -y install tasksh && \
  rm -rf /var/lib/apt/lists/*

COPY taskrc /root/.taskrc

ENTRYPOINT tasksh

VOLUME /root/.tasksh
