FROM eclipse/stack-base:ubuntu
ENV CLANGD_VERSION="6.0"
RUN wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | sudo apt-key add - && \
    sudo apt-add-repository "deb http://apt.llvm.org/xenial/ llvm-toolchain-xenial-${CLANGD_VERSION} main" && \
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test && \
    sudo apt-get update && \
    sudo apt-get install g++-8 gcc-8 make gdb gdbserver clang-${CLANGD_VERSION} clang-tools-${CLANGD_VERSION} -y && \
    sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 60 --slave /usr/bin/g++ g++ /usr/bin/g++-8 && \
    sudo apt-get clean && \
    sudo apt-get -y autoremove && \
    sudo rm -rf /var/lib/apt/lists/* && \
    sudo ln -s /usr/bin/clangd-${CLANGD_VERSION} /usr/bin/clangd && \
    sudo ln -s /usr/bin/clang-${CLANGD_VERSION} /usr/bin/clang && \
    sudo ln -s /usr/bin/clang++-${CLANGD_VERSION} /usr/bin/clang++
