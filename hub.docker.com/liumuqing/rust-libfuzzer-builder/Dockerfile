FROM ubuntu:18.04

# enable source
RUN sed -i 's/# deb-src/deb-src/g' /etc/apt/sources.list
RUN apt-get update && apt-get install -y wget gnupg2 git

RUN echo "deb http://apt.llvm.org/bionic/ llvm-toolchain-bionic-8 main" >> /etc/apt/sources.list
RUN echo "deb-src http://apt.llvm.org/bionic/ llvm-toolchain-bionic-8 main" >> /etc/apt/sources.list
RUN echo "deb http://apt.llvm.org/bionic/ llvm-toolchain-bionic-9 main" >> /etc/apt/sources.list
RUN echo "deb-src http://apt.llvm.org/bionic/ llvm-toolchain-bionic-9 main" >> /etc/apt/sources.list
RUN wget --quiet -O llvm-snapshot.gpg.key https://apt.llvm.org/llvm-snapshot.gpg.key && apt-key add llvm-snapshot.gpg.key && rm llvm-snapshot.gpg.key

RUN apt-get update && apt-get install -y clang-9 libfuzzer-9-dev
RUN apt-get install && DEBIAN_FRONTEND=noninteractive apt-get install -y apt-build


RUN wget --quiet -O rustup.sh https://sh.rustup.rs && chmod +x rustup.sh && ./rustup.sh -y --default-toolchain nightly && rm rustup.sh
ENV PATH="/root/.cargo/bin:${PATH}"

# install clang_wrapper
COPY clang_wrapper /opt/clang_wrapper
RUN clang-9 /opt/clang_wrapper/main.c -O3 -o /opt/clang_wrapper/clang_wrapper

# replace cc, cxx, gcc to clang_wrapper (let's just left clang-8 to be the original clang)
RUN update-alternatives --install /usr/bin/c89 c89 /opt/clang_wrapper/clang_wrapper 1024
RUN update-alternatives --install /usr/bin/c99 c99 /opt/clang_wrapper/clang_wrapper 1024
RUN update-alternatives --install /usr/bin/c++ c++ /opt/clang_wrapper/clang_wrapper 1024
RUN update-alternatives --install /usr/bin/cc cc /opt/clang_wrapper/clang_wrapper 1024
RUN update-alternatives --install /usr/bin/g++ g++ /opt/clang_wrapper/clang_wrapper 1024
RUN update-alternatives --install /usr/bin/gcc gcc /opt/clang_wrapper/clang_wrapper 1024
RUN update-alternatives --install /usr/bin/clang++ clang++ /opt/clang_wrapper/clang_wrapper 1024
RUN update-alternatives --install /usr/bin/clang clang /opt/clang_wrapper/clang_wrapper 1024


# now all rust compiled code will instrumented also
COPY cargo_config/config /root/.cargo/config
ENV ASAN_OPTIONS="detect_leaks=0"

# This is for libfuzzer-sys
RUN test -f "/usr/lib/llvm-9/lib/libFuzzer.a"
ENV CUSTOM_LIBFUZZER_PATH="/usr/lib/llvm-9/lib/libFuzzer.a"

WORKDIR /root

COPY ./example_fuzzers /root/example_fuzzers
RUN cd /root/example_fuzzers/sqlite && cargo build --release
RUN cd /root/example_fuzzers/imagequant && cargo build --release
RUN cd /root/example_fuzzers/openssl && cargo build --release
RUN rm -rf /root/example_fuzzers
