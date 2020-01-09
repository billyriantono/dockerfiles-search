FROM ubuntu:18.10

MAINTAINER Isaac A, <isaac@isaacs.site>

ENV DEBIAN_FRONTEND noninteractive

RUN dpkg --add-architecture i386 && \
    sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list && \
    sed -i 's/security.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list && \
    apt update && \
    apt upgrade -y && \
    apt install -y curl wget screen htop unzip wget lib32stdc++6 mono-runtime mono-reference-assemblies-2.0 libdb1-compat tzdata && \
    useradd -d /home/container -m container

USER container
ENV  USER container
ENV  HOME /home/container

WORKDIR /home/container

COPY ./entrypoint.sh /entrypoint.sh

CMD ["/bin/bash", "/entrypoint.sh"]
