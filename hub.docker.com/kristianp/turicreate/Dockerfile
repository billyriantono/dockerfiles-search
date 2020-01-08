FROM ubuntu:18.04

RUN echo "deb mirror://mirrors.ubuntu.com/mirrors.txt bionic main restricted universe multiverse" > /etc/apt/sources.list && \
    echo "deb mirror://mirrors.ubuntu.com/mirrors.txt bionic-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb mirror://mirrors.ubuntu.com/mirrors.txt bionic-security main restricted universe multiverse" >> /etc/apt/sources.list && \
    apt-get update && \
	apt-get install  --no-install-recommends  python3=3.6.7-1~18.04 python3-pip libatlas3-base python3-setuptools -y && \
	pip3 install -U wheel jupyterlab turicreate && \
	mkdir /workdir/ && \
	export PATH=$PATH:~/.local/bin/

EXPOSE 8888

WORKDIR /workdir/

VOLUME [ "/workdir" ]

CMD [ "/bin/bash" ]