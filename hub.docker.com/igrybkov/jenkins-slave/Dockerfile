FROM evarga/jenkins-slave

RUN apt-get update && \
    apt-get install -y git sqlite3 libsqlite3-dev build-essential gcc g++ && \
    apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN apt-get update && \
    apt-get install -y libc6-dev-x32 libc6-dev-i386 mingw-w64 mingw-w64-x86-64-dev mingw32 && \
    apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN apt-get update && \
    apt-get install -y gcc-mingw-w64 gcc-mingw-w64-i686 gcc-multilib gcc-mingw-w64-x86-64 gccgo gccgo-multilib gcc-arm-linux-gnueabi libboost-thread-dev && \
    apt-get clean -y && rm -rf /var/lib/apt/lists/*
