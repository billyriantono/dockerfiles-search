FROM centos:centos7.5.1804

ENV PROTOBUF_VER=3.10.1
ENV PROTOBUF_URL=https://github.com/protocolbuffers/protobuf/releases/download
ENV PROTOBUF_SRC_FILE=protobuf-cpp-${PROTOBUF_VER}.tar.gz
ENV PROTOBUF_ARTIFACT=protobuf-${PROTOBUF_VER}.tgz

RUN yum -y -q install   cmake   \
                        gcc-c++ \
                        make    \
                        wget

VOLUME /var/tmp

WORKDIR /tmp
RUN wget --quiet ${PROTOBUF_URL}/v${PROTOBUF_VER}/${PROTOBUF_SRC_FILE}  \
    && tar xzf ${PROTOBUF_SRC_FILE}                                     \
    && cd /tmp/protobuf-${PROTOBUF_VER}                                 \
    && ./configure                                                      \
    && make                                                             \
    && rm -rf /usr/local/*                                              \
    && make install                                                     \
    && rm -rf /tmp/*
    
WORKDIR /usr/local
RUN tar czf /tmp/${PROTOBUF_ARTIFACT} ./include ./lib ./bin

CMD cp /tmp/${PROTOBUF_ARTIFACT} /var/tmp/
