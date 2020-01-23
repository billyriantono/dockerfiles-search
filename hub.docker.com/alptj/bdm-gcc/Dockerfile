FROM debian:stable-slim

RUN apt update && apt upgrade -y \
    && apt install -y \
        build-essential \
        cmake \
        qt5-default \
        qtbase5-dev \
        qttools5-dev \
        python3-pip \
        ninja-build \
        curl \
    && pip3 install conan \
    && conan profile new --detect default \
    && conan profile update settings.compiler.libcxx=libstdc++11 default \
    && conan remote add bincrafters https://api.bintray.com/conan/bincrafters/public-conan
