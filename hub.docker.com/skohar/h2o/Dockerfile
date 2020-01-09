FROM buildpack-deps

RUN apt-get update && apt-get install -y \
    cmake \
    && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/h2o/h2o \
    && cd h2o \
    && git submodule update --init --recursive \
    && cmake . \
    && make install h2o \
    && cd .. \
    && rm -rf /h2o

