FROM centos:7
MAINTAINER <PengShaw, hhxp9106@gmail.com>

RUN mkdir -p /home/leanote
WORKDIR  /home/leanote
RUN cd /home/leanote && \
    yum update -y && \
    yum install wget tar -y && \
    wget https://sourceforge.net/projects/leanote-bin/files/2.6.1/leanote-linux-amd64-v2.6.1.bin.tar.gz/download -O leanote-linux-amd64-v2.6.1.bin.tar.gz && \
    tar -xzvf leanote-linux-amd64-v2.6.1.bin.tar.gz && \
    wget https://downloads.wkhtmltopdf.org/0.12/0.12.5/wkhtmltox-0.12.5-1.centos7.x86_64.rpm
