FROM centos:centos7.5.1804

COPY --from=kerrytjohnson/protobuf:3.10.1   /usr/local/ /usr/local/
COPY --from=kerrytjohnson/protobuf-c:1.3.2  /usr/local/ /usr/local/

ENV NATS_C_VER=2.1.0
ENV NATS_C_URL=https://github.com/nats-io/nats.c/archive
ENV NATS_C_SRC_FILE=v${NATS_C_VER}.tar.gz
ENV NATS_C_ARTIFACT=nats-c-${NATS_C_VER}.tgz
ENV NATS_C_LINKER_FLAGS=-lprotobuf-c

RUN yum -y -q install   cmake           \
                        gcc-c++         \
                        make            \
                        openssl-devel   \
                        wget

VOLUME /var/tmp
    
WORKDIR /tmp
RUN wget --quiet ${NATS_C_URL}/${NATS_C_SRC_FILE}                       \
    && tar xzf ${NATS_C_SRC_FILE}                                       \
    && mkdir nats.c-${NATS_C_VER}/build                                 \
    && cd /tmp/nats.c-${NATS_C_VER}/build                               \
    && cmake    -DCMAKE_EXE_LINKER_FLAGS="${NATS_C_LINKER_FLAGS}" ..    \
                -DCMAKE_INSTALL_LIBDIR=lib                              \
    && make                                                             \
    && rm -rf /usr/local/*                                              \
    && make install

WORKDIR /usr/local
RUN tar czf /tmp/${NATS_C_ARTIFACT} ./include ./lib

CMD cp /tmp/${NATS_C_ARTIFACT} /var/tmp/
