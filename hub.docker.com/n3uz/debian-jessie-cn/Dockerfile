FROM debian:jessie

ENV TZ=Asia/Shanghai

RUN apt update && apt install -y wget \
	&& wget -q http://mirrors.163.com/.help/sources.list.jessie -O /etc/apt/sources.list\
	&& rm -rf /var/lib/apt/lists/*

ADD bashrc /root/.bashrc

WORKDIR /root

CMD ["bash"]
