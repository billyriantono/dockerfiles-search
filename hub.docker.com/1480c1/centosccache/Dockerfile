FROM centos:7
LABEL maintainer="Christopher Degawa <ccom@randomderp.com>" \
    name="ccacheBuilds" \
    description="ccache container for ci" \
    vcs-url="https://github.com/1480c1/ccacheBuilds" \
    License="MIT License" \
    version="0.0.1"

ARG CC=gcc
ARG CXX=g++

RUN yum install -y \
    epel-release-7-11 && \
    yum install -y \
    make-3.82-23.el7 \
    clang-3.4.2-9.el7 \
    gcc-4.8.5-36.el7_6.2 \
    gcc-c++-4.8.5-36.el7_6.2 \
    ccache-3.3.4-1.el7
RUN mkdir /root/.ccache/ && \
    ln -s /root/.ccache/ /ccache && \
    yum erase -y \
    make && \
    yum clean all && \
    rm -rf /var/cache/yum;

VOLUME [ "/ccache" ]

ENTRYPOINT [ "/bin/bash" ]
CMD [ "-l" ]
