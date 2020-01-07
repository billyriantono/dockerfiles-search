FROM ubuntu:14.04
MAINTAINER Peter Ericson <pdericson@gmail.com>

RUN TINI_VERSION=0.9.0; \
apt-get update && \
apt-get upgrade -y && \
apt-get install --no-install-recommends -y ca-certificates curl && \
curl -fLO https://github.com/krallin/tini/releases/download/v$TINI_VERSION/tini_$TINI_VERSION.deb && \
dpkg -i tini_$TINI_VERSION.deb && \
rm -f tini_$TINI_VERSION.deb && \
rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["/usr/bin/tini", "-g", "-v", "--"]
CMD ["/bin/bash"]
