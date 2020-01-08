FROM ubuntu:16.04

RUN echo "deb http://cn.archive.ubuntu.com/ubuntu/ xenial main restricted universe multiverse" > /etc/apt/sources.list \
	&& echo "deb http://cn.archive.ubuntu.com/ubuntu/ xenial-security main restricted universe multiverse" >>/etc/apt/sources.list \
	&& echo "deb http://cn.archive.ubuntu.com/ubuntu/ xenial-updates main restricted universe multiverse" >>/etc/apt/sources.list \
	&& echo "deb http://cn.archive.ubuntu.com/ubuntu/ xenial-backports main restricted universe multiverse" >>/etc/apt/sources.list \
	&& echo "deb http://cn.archive.ubuntu.com/ubuntu/ xenial-proposed main restricted universe multiverse" >>/etc/apt/sources.list \
	&& echo "deb-src http://cn.archive.ubuntu.com/ubuntu/ xenial main restricted universe multiverse" >>/etc/apt/sources.list \
	&& echo "deb-src http://cn.archive.ubuntu.com/ubuntu/ xenial-security main restricted universe multiverse" >>/etc/apt/sources.list \
	&& echo "deb-src http://cn.archive.ubuntu.com/ubuntu/ xenial-updates main restricted universe multiverse" >>/etc/apt/sources.list \
	&& echo "deb-src http://cn.archive.ubuntu.com/ubuntu/ xenial-backports main restricted universe multiverse" >>/etc/apt/sources.list \
	&& echo "deb-src http://cn.archive.ubuntu.com/ubuntu/ xenial-proposed main restricted universe multiverse" >>/etc/apt/sources.list \
	&& apt update \
	&& apt install  -y tzdata \
	&& rm -rf /var/lib/apt/lists/*

ENV TZ=Asia/Shanghai

WORKDIR /root

ADD bashrc /root/.bashrc

CMD ["bash"]
