FROM centos:centos7.5.1804

ARG NATS_CPP_VER=dev

ENV SCONS="/usr/bin/env python3 /usr/local/bin/scons"
ENV SCONSTRUCT="/usr/local/scons-wrapper/SConstruct"

COPY --from=kerrytjohnson/scons-wrapper:latest  /usr/local/scons-wrapper/   /usr/local/scons-wrapper/
COPY --from=kerrytjohnson/protobuf:3.10.1       /usr/local/                 /usr/local/
COPY --from=kerrytjohnson/protobuf-c:1.3.2      /usr/local/                 /usr/local/
COPY --from=kerrytjohnson/nats-c:2.1.0          /usr/local/                 /usr/local/
COPY --from=kerrytjohnson/boost:1.71.0          /usr/local/                 /usr/local/

RUN echo "/usr/local/lib" >> /etc/ld.so.conf.d/usr_local_lib.conf       \
    && ldconfig

RUN echo "[main]"                               >> /etc/yum/yum.conf    \
    && echo "skip_missing_names_on_install=0"   >> /etc/yum/yum.conf    \
    && echo "skip_missing_names_on_update=0"    >> /etc/yum/yum.conf

RUN yum -y -q install   gcc-c++     \
                        file        \
                        less        \
                        make        \
                        python3     \  
                        python3-pip \
                        wget        \
                        which

RUN python3 -m pip install pyyaml scons

WORKDIR /tmp/nats-cpp

COPY context/   /
COPY cfg/       /tmp/nats-cpp/cfg
COPY src/       /tmp/nats-cpp/src

RUN ${SCONS} -f ${SCONSTRUCT}                      \
    && ${SCONS} -f ${SCONSTRUCT} install-nats-cpp
    
WORKDIR /usr/local
RUN tar czf /tmp/nats-cpp-${NATS_CPP_VER}.tgz ./include/nats-cpp ./lib/libnats-cpp*

