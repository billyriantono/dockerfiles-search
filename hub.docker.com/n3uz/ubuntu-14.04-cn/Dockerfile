FROM ubuntu:14.04

RUN echo "deb http://mirrors.aliyun.com/ubuntu/ trusty main restricted" > /etc/apt/sources.list \
    && echo "deb http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted" >> /etc/apt/sources.list \
    && echo "deb http://mirrors.aliyun.com/ubuntu/ trusty universe" >> /etc/apt/sources.list \
    && echo "deb http://mirrors.aliyun.com/ubuntu/ trusty-updates universe" >> /etc/apt/sources.list \
    && echo "deb http://mirrors.aliyun.com/ubuntu/ trusty multiverse" >> /etc/apt/sources.list \
    && echo "deb http://mirrors.aliyun.com/ubuntu/ trusty-updates multiverse" >> /etc/apt/sources.list \
    && echo "deb http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse" >> /etc/apt/sources.list \
    && echo "deb http://security.ubuntu.com/ubuntu/ trusty-security main restricted" >> /etc/apt/sources.list \
    && echo "deb http://security.ubuntu.com/ubuntu/ trusty-security universe" >> /etc/apt/sources.list \
    && echo "deb http://security.ubuntu.com/ubuntu/ trusty-security multiverse" >> /etc/apt/sources.list \
	&& apt update \
    && apt install  -y tzdata \
    && rm -rf /var/lib/apt/lists/*

ENV TZ=Asia/Shanghai
WORKDIR /root
ADD bashrc /root/.bashrc
CMD ["bash"]
