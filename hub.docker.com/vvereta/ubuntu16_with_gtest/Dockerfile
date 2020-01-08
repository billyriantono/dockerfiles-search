FROM ubuntu:16.04

RUN apt-get update && apt-get install -y --no-install-recommends \
    gcc \
    g++ \
    make \
    cmake \
    libgtest-dev \
    gcovr \
    && apt clean

# Compile GTest libraries
WORKDIR /usr/src/gtest
RUN cmake .
RUN make
RUN mv libg* /usr/lib/
