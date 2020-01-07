FROM gcc:latest

RUN set -ex; \
	mkdir -p /opt/cmake; \
	curl -fSL "https://cmake.org/files/v3.10/cmake-3.10.1-Linux-x86_64.tar.gz" | tar -xzC /opt/cmake --strip-components=1;

ENV PATH "$PATH:/opt/cmake/bin"
