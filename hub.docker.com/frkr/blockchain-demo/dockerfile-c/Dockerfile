FROM debian:buster-slim

ENV EW_VERSION 7.10
ENV EW_DIR /opt/earthworm/earthworm-${EW_VERSION}
ENV PATH ${EW_DIR}/bin:${PATH}

ENV EW_HOME ${EW_DIR}
ENV EW_INSTALLATION=INST_NMX
ENV EW_LOG=/earthworm/log
ENV EW_PARAMS=/earthworm/params
ENV SYS_NAME=NMX

ADD earthworm_7.10_amd64.deb /earthworm_7.10_amd64.deb
RUN apt update && apt install libgfortran4 /earthworm_7.10_amd64.deb -y

VOLUME /bulletins
VOLUME /earthworm

ENTRYPOINT /bin/startstop
