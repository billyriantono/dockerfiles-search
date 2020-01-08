FROM debian:stretch

RUN apt-get update && apt-get install -y --no-install-recommends gnupg wget ca-certificates
RUN wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add -
RUN echo "deb http://apt.llvm.org/stretch/ llvm-toolchain-stretch-7 main" >> /etc/apt/sources.list.d/main.list
RUN apt-get update && apt-get install -y --no-install-recommends clang-7 make cmake
ENV CXX=/usr/bin/clang++-7