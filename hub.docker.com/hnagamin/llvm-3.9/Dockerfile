FROM ubuntu:16.04
WORKDIR /
RUN apt-get update
RUN \
 apt-get install -y clang cmake curl file python ninja-build xz-utils --no-install-recommends && \
 curl http://releases.llvm.org/3.9.1/llvm-3.9.1.src.tar.xz | tar xJf - && \
 mv /llvm-3.9.1.src /llvm && \
 curl http://releases.llvm.org/3.9.1/compiler-rt-3.9.1.src.tar.xz | tar xJf - && \
 mv /compiler-rt-3.9.1.src /llvm/projects/compiler-rt && \
 curl http://releases.llvm.org/3.9.1/cfe-3.9.1.src.tar.xz | tar xJf - && \
 mv /cfe-3.9.1.src /llvm/tools/clang && \
 mkdir llvm/build && \
 cd llvm/build && \
 CC=clang CXX=clang++ cmake -G Ninja -DCMAKE_BUILD_TYPE=MinSizeRel -DLLVM_TARGETS_TO_BUILD=X86 .. && \
 (ninja || ninja -j1) && \
 ninja install && \
 rm -rf /llvm /build && \
 apt-get remove --auto-remove -y clang curl file ninja-build xz-utils
RUN apt-get install -y build-essential make libboost-all-dev --no-install-recommends
