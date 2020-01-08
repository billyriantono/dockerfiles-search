FROM sys42/docker-build-essentials:1.0.0
MAINTAINER Tom Nussbaumer <thomas.nussbaumer@gmx.net>

ADD ruby20/ruby191/rubymulti/install-data /tmp_build

RUN /tmp_build/prepare.sh && \
    /tmp_build/rubyX.sh 2.1   181 51 && \
    /tmp_build/finalize.sh
