FROM ubuntu:latest

RUN apt-get -y update \
    && apt-get install -y software-properties-common \
    && add-apt-repository -y ppa:ubuntu-toolchain-r/test \
    && apt-get -y update && apt-get install -y --no-install-recommends \
        build-essential \
        cmake \
        qt5-default \
        qttools5-dev-tools \
        libqt5sql5-sqlite \
        libqt5sql5-mysql \
        python-pip \
        python-setuptools \
    && pip install conan \
    && rm -rf /var/lib/apt/lists/*

CMD ["/bin/bash"]
