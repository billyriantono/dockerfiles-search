FROM debian:stretch-slim AS fswatch-build-stage

RUN apt-get update && apt-get install -y wget make g++

ENV ROOT_HOME /root
WORKDIR ${ROOT_HOME}
RUN wget https://github.com/emcrisostomo/fswatch/releases/download/1.13.0/fswatch-1.13.0.tar.gz && \
    tar xvf fswatch-1.13.0.tar.gz

WORKDIR ${ROOT_HOME}/fswatch-1.13.0
RUN ./configure LDFLAGS="-static" && make && mv fswatch/src/fswatch /

FROM scratch
COPY --from=fswatch-build-stage /fswatch /usr/local/bin

# Example usage of this image
# FROM KevinClaudius/fswatch-docker AS fswatch-stage
# COPY --from=fswatch-stage /fswatch /usr/local/bin
