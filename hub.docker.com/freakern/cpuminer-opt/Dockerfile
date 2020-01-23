# Build
FROM ubuntu:16.04 as builder

RUN apt-get update \
  && apt-get install -y \
    build-essential \
    libssl-dev \
    libgmp-dev \
    libcurl4-openssl-dev \
    libjansson-dev \
    automake \
    git \
  && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/JayDDee/cpuminer-opt.git cpuminer \
    && cd cpuminer \
    && ./build.sh

# App
FROM ubuntu:16.04

RUN apt-get update \
  && apt-get install -y \
    libcurl3 \
    libjansson4 \
  && rm -rf /var/lib/apt/lists/*

COPY --from=builder cpuminer/cpuminer .
ENTRYPOINT ["./cpuminer"]
CMD ["-h"]
