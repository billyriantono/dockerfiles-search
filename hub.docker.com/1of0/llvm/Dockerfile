FROM ubuntu:trusty

RUN apt-get update
RUN apt-get install -yyy wget

RUN wget -O - http://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add -
COPY apt/llvm.list /etc/apt/sources.list.d/llvm.list
COPY apt/llvm.pref /etc/apt/preferences.d/llvm

RUN apt-get update
RUN apt-get upgrade -yyy
RUN apt-get install -yyy clang-3.9 libllvm3.9 libclang-3.9-dev llvm-3.9 llvm-3.9-tools zlib1g-dev libncurses5-dev

RUN apt-get install -yyy git cmake ccache

ENV PATH /usr/lib/llvm-3.9/bin:$PATH
