FROM ubuntu:latest
MAINTAINER Tran Quoc Cuong <trquoccuong@gmail.com>

# Install related packages
RUN apt-get update && \
    apt-get install -y git cmake ninja-build clang uuid-dev libicu-dev icu-devtools libbsd-dev libedit-dev libxml2-dev libsqlite3-dev swig libpython-dev libncurses5-dev pkg-config


# Install C++14
RUN apt-get install -y clang-3.6 && \
    update-alternatives --install /usr/bin/clang clang /usr/bin/clang-3.6 100 && \
    update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-3.6 100 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Clone latest from git

RUN mkdir myswift && \
    cd myswift && \
    git clone https://github.com/apple/swift.git swift && \
    git clone https://github.com/apple/swift-llvm.git llvm && \
    git clone https://github.com/apple/swift-clang.git clang && \
    git clone https://github.com/apple/swift-lldb.git lldb && \
    git clone https://github.com/apple/swift-cmark.git cmark && \
    git clone https://github.com/apple/swift-llbuild.git llbuild && \
    git clone https://github.com/apple/swift-package-manager.git swiftpm && \
    git clone https://github.com/apple/swift-corelibs-xctest.git && \
    git clone https://github.com/apple/swift-corelibs-foundation.git && \
    ./swift/utils/build-script -R 
RUN    mv myswift/build/  coreswift && \
    rm -rf myswift/ /tmp/* /var/tmp/*
    
ENV PATH "/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/coreswift/Ninja-ReleaseAssert/swift-linux-x86_64/bin"

RUN swift --version
    
    
