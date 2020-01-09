FROM gcc:8

#RUN apt-get update && apt-get install -y --no-install-recommends \
#    cmake \
#  && apt-get clean \
#  && rm -rf /var/lib/apt/lists/*

RUN curl https://cmake.org/files/v3.11/cmake-3.11.3-Linux-x86_64.sh -o /tmp/curl-install.sh \
      && chmod u+x /tmp/curl-install.sh \
      && mkdir /usr/bin/cmake \
      && /tmp/curl-install.sh --skip-license --prefix=/usr/bin/cmake \
      && rm /tmp/curl-install.sh


RUN apt-get update && apt-get install -y --no-install-recommends \
    libboost-all-dev \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y --no-install-recommends \
    zlib1g-dev libbz2-dev libsnappy-dev \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

ENV PATH="/usr/bin/cmake/bin:${PATH}"

