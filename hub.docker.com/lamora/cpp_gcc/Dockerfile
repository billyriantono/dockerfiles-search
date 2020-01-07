FROM gitpod/workspace-full:latest
USER root
ENV CLANGD_VERSION="9"
RUN wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add - && \
	add-apt-repository -y ppa:mhier/libboost-latest && \
	apt-key adv --keyserver keyserver.ubuntu.com --recv-keys ABF5BD827BD9BF62 && \
	apt-add-repository "deb http://nginx.org/packages/ubuntu/ `lsb_release -sc` nginx" && \
	apt-add-repository "deb http://apt.llvm.org/`lsb_release -sc`/ llvm-toolchain-`lsb_release -sc` main"
RUN	apt update && \
    apt install -y g++ gcc make gdb gdbserver \
		clang-tools-${CLANGD_VERSION} libllvm${CLANGD_VERSION} llvm-${CLANGD_VERSION} llvm-${CLANGD_VERSION}-dev clang++-${CLANGD_VERSION} clang-tools-${CLANGD_VERSION} libclang-${CLANGD_VERSION}-dev libclang1-${CLANGD_VERSION} \
		cmake libboost1.68-dev nginx dnsutils iputils-ping ninja-build libpoco-dev ragel && \
    apt clean && \
    rm -rf /var/lib/apt/lists/* && rm -rf /var/cache/apt/* && rm -rf /var/lib/apt/lists/* && rm -rf /tmp/*