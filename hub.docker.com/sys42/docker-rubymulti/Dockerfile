FROM sys42/docker-build-essentials:1.1.0
MAINTAINER Tom Nussbaumer <thomas.nussbaumer@gmx.net>

ADD install-data /tmp_build

RUN /tmp_build/prepare.sh && \
    /tmp_build/rubyX.sh 1.9.1 161 31 && \
    /tmp_build/rubyX.sh 2.0   171 41 && \
    /tmp_build/rubyX.sh 2.1   181 51 && \
    /tmp_build/rubyX.sh 2.2   191 61 && \
    /tmp_build/finalize.sh
