FROM centos:centos7.5.1804

COPY --from=kerrytjohnson/protobuf:3.10.1 /usr/local/ /usr/local/

ENV PROTOBUF_C_VER=1.3.2
ENV PROTOBUF_C_URL=https://github.com/protobuf-c/protobuf-c/releases/download
ENV PROTOBUF_C_SRC_FILE=protobuf-c-${PROTOBUF_C_VER}.tar.gz
ENV PROTOBUF_C_ARTIFACT=protobuf-c-${PROTOBUF_C_VER}.tgz

RUN yum -y -q install   gcc-c++ \
                        make    \
                        wget

VOLUME /var/tmp

WORKDIR /tmp
RUN wget --quiet ${PROTOBUF_C_URL}/v${PROTOBUF_C_VER}/${PROTOBUF_C_SRC_FILE}    \
    && tar xzf ${PROTOBUF_C_SRC_FILE}                                           \
    && cd /tmp/protobuf-c-${PROTOBUF_C_VER}                                     \
    && PKG_CONFIG_PATH=/usr/local/lib/pkgconfig ./configure                     \
    && make                                                                     \
    && make install                                                             \
    && rm -rf   /usr/local/include/google                                       \
                /usr/local/lib/libprotobuf-lite.*                               \
                /usr/local/lib/libprotobuf.*                                    \
                /usr/local/lib/libprotoc.*                                      \
                /usr/local/lib/pkgconfig/protobuf*                              \
                /usr/local/bin/*                                                \
    && rm -rf /tmp/*
    
WORKDIR /usr/local
RUN tar czf /tmp/${PROTOBUF_C_ARTIFACT} ./include ./lib

CMD cp /tmp/${PROTOBUF_C_ARTIFACT} /var/tmp/
