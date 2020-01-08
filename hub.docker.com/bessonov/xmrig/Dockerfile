FROM ubuntu:16.04 as builder

RUN apt-get update \
		&& apt-get install -y software-properties-common \
		&& add-apt-repository ppa:jonathonf/gcc-7.1 \
		&& apt-get update \
		&& apt-get install -y gcc-7 g++-7 \
		&& apt-get install -y build-essential cmake libuv1-dev libmicrohttpd-dev \
		&& apt-get clean \
		&& rm -rf /var/lib/apt/lists/*

WORKDIR xmrig

RUN mkdir build

ADD CMakeLists.txt CMakeLists.txt
ADD cmake cmake
ADD res res
ADD src src

WORKDIR build

RUN cmake .. -DCMAKE_C_COMPILER=gcc-7 -DCMAKE_CXX_COMPILER=g++-7
RUN make

FROM ubuntu:16.04

RUN apt-get update \
		&& apt-get install -y libuv1 libmicrohttpd10 \
		&& apt-get clean \
		&& rm -rf /var/lib/apt/lists/*

COPY --from=builder /xmrig/build/xmrig /usr/local/bin/xmrig

ENTRYPOINT ["xmrig"]
CMD []
