FROM debian:testing-slim

RUN ["/bin/bash", "-c", "set -e ; set -o pipefail ; apt-get update ; apt-get dist-upgrade -y ; apt-get autoremove -y ; apt-get install -y sudo locales build-essential git ccache libcrypto++ meson pkg-config libunwind-dev g++-8 clang-6.0 lldb-6.0 gdb valgrind doctest-dev libboost-all-dev curl iputils-ping vim tcpdump man-db"]

RUN ["/bin/bash", "-c", "sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen; dpkg-reconfigure --frontend=noninteractive locales; update-locale LANG=en_US.UTF-8"]

CMD ["/bin/bash", "-l"]
WORKDIR /project

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
ENV CCACHE_DIR=/project/.ccache
