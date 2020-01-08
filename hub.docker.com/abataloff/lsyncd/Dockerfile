FROM ubuntu:16.04
RUN apt-get update && \
    apt-get -y --force-yes --no-install-recommends install \
    ca-certificates \
    git \
    rsync \
    ssh \
    lua5.3 \
    lua5.3-dev \
    cmake \
    gcc \
    build-essential
RUN git clone https://github.com/axkibe/lsyncd.git
WORKDIR lsyncd
RUN cmake .
RUN make
RUN make install
ENTRYPOINT lsyncd /lsyncd/lsyncd.config