FROM ubuntu:18.10
RUN sed -i.bak -e "s%http://[^ ]+%http://ftp.jaist.ac.jp/pub/Linux/ubuntu/%g" /etc/apt/sources.list \
  && apt update \
  && apt install --no-install-recommends -y gcc-8 g++-8 make clang-6.0 libc++-dev libc++abi-dev libboost-all-dev \
  && ln -s /usr/bin/gcc-8 /bin/gcc \
  && ln -s /usr/bin/g++-8 /bin/g++ \
  && ln -s /usr/bin/clang-6.0 /bin/clang \
  && ln -s /usr/bin/clang++-6.0 /bin/clang++ \
  && apt clean \
  && rm -rf /var/cache/* \
  && rm -rf /var/lib/apt/lists/*
