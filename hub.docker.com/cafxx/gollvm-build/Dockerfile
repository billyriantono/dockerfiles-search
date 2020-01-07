# Dockerfile that builds a release of gollvm from the tip (master)
# see https://go.googlesource.com/gollvm/+/master#setting-up-a-gollvm-work-area
# note that intermediate steps are preserved, so the image is going to be on the big side.
#
# gollvm is installed in $GOLLVM_PATH and is added to the PATH, so you can simply run `go`.
#
# By default gollvm builds dynamic executables; if you want to build static executables
# (the standard behavior of the gc go compiler) you need to build using the static flag:
# `go build -gccgoflags="--static" [...]`

FROM ubuntu:xenial

# use bash -- cmake fails otherwise
SHELL ["/bin/bash", "-c"]
ENV SHELL=/bin/bash

RUN apt -qq -o=Dpkg::Use-Pty=0 update && \
    apt -qq -o=Dpkg::Use-Pty=0 install --no-install-recommends -y git ninja-build cmake build-essential clang autoconf ca-certificates python && \
    apt -qq -o=Dpkg::Use-Pty=0 list --installed

RUN mkdir -p /gollvm/src /gollvm/build /gollvm/install

COPY src/llvm         /gollvm/src/llvm
COPY src/gollvm       /gollvm/src/llvm/tools/gollvm
COPY src/gofrontend   /gollvm/src/llvm/tools/gollvm/gofrontend
COPY src/libffi       /gollvm/src/llvm/tools/gollvm/libgo/libffi
COPY src/libbacktrace /gollvm/src/llvm/tools/gollvm/libgo/libbacktrace

RUN cd /gollvm/build && cmake -DCMAKE_INSTALL_PREFIX=/gollvm/install -DCMAKE_BUILD_TYPE=Release -DLLVM_TARGETS_TO_BUILD="X86" -DLLVM_USE_LINKER=gold -G Ninja /gollvm/src/llvm
RUN cd /gollvm/build && ninja gollvm
RUN cd /gollvm/build && ninja GoBackendCoreTests && tools/gollvm/unittests/BackendCore/GoBackendCoreTests
RUN cd /gollvm/build && ninja install-gollvm

ENV GOLLVM_PATH=/gollvm/install
ENV LD_LIBRARY_PATH=$GOLLVM_PATH/lib64
ENV PATH=$GOLLVM_PATH/bin:$PATH
