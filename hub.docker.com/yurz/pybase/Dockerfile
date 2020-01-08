FROM ubuntu:18.04

LABEL authors="Yuri Zhylyuk yuri@zhylyuk.com"

RUN \
    apt-get -y update \
    && apt-get -y upgrade \
    && apt-get -y install apt-utils \
        wget curl nano sshpass libpq-dev bzip2 smbclient tzdata \ 
    && apt-get -y install --reinstall ca-certificates \
    && update-ca-certificates \
    && cd ~ \
    && curl -O https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh \
    && chmod +x ~/Miniconda3-latest-Linux-x86_64.sh \
    && ~/Miniconda3-latest-Linux-x86_64.sh -p /miniconda -b \
    && rm ~/Miniconda3-latest-Linux-x86_64.sh \
    && PATH=/miniconda/bin:$PATH \
    && conda clean -y -a \
    && apt-get clean autoclean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/{cache,log}/
ENV PATH /miniconda/bin:$PATH
