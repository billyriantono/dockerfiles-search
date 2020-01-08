FROM debian:jessie
RUN echo "deb http://llvm.org/apt/trusty/ llvm-toolchain-trusty-3.6 main" | tee /etc/apt/sources.list.d/llvm.list
RUN apt-get update && apt-get install -y wget git
RUN wget -O - http://llvm.org/apt/llvm-snapshot.gpg.key | apt-key add -
RUN apt-get update
RUN apt-get install -y cmake llvm-3.5 clang-3.5 lldb-3.6 lldb-3.6-dev libunwind8 \
    libunwind8-dev gettext libicu-dev liblttng-ust-dev libcurl4-openssl-dev libssl-dev uuid-dev
RUN mkdir git
WORKDIR /root/git
RUN git clone https://github.com/dotnet/coreclr.git
WORKDIR /root/git/coreclr
RUN git checkout 56ab756
RUN ./build.sh
RUN export PATH=$PATH:/root/git/coreclr/Tools/
