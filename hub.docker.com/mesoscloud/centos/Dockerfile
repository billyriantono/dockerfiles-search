FROM centos:7
MAINTAINER Peter Ericson <pdericson@gmail.com>

RUN TINI_VERSION=0.9.0; \
yum upgrade -y && \
rpm -i https://github.com/krallin/tini/releases/download/v$TINI_VERSION/tini_$TINI_VERSION.rpm && \
yum clean all

ENTRYPOINT ["/usr/bin/tini", "-g", "-v", "--"]
CMD ["/bin/bash"]
