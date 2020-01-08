FROM sys42/docker-build-essentials:1.0.0
MAINTAINER Tom Nussbaumer <thomas.nussbaumer@gmx.net>

ADD rubymulti/install-data /tmp_build

RUN /tmp_build/prepare.sh && \
    /tmp_build/rubyX.sh 1.9.1 161 31 && \
    /tmp_build/finalize.sh
