FROM sys42/docker-build-essentials:1.1.0
MAINTAINER Tom Nussbaumer <thomas.nussbaumer@gmx.net>

ADD ruby191/rubymulti/install-data /tmp_build

RUN /tmp_build/prepare.sh && \
    /tmp_build/rubyX.sh 2.0   171 41 && \
    /tmp_build/finalize.sh
