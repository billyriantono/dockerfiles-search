FROM    centos:7

RUN     yum update -y
RUN     yum group install "Development Tools" -y
RUN     yum install -y gcc \
                       clang \
                       wget \
                       make \
                       openssl-devel \
                       llvm-toolset-7

RUN     curl https://sh.rustup.rs -sSf | sh -s -- -y --default-toolchain nightly

# Relou
RUN     wget https://cmake.org/files/v3.13/cmake-3.13.4-Linux-x86_64.tar.gz
RUN     tar -zxvf cmake-3.13.4-Linux-x86_64.tar.gz
ENV     PATH "/cmake-3.13.4-Linux-x86_64/bin:$PATH"
