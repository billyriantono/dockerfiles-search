FROM golang:1.6-wheezy
USER root

# Source: me
RUN apt-get update && apt-get install -y --no-install-recommends \
        p7zip-full \
        python \
        git \
        openssh-client \
        sudo \
        build-essential \
	&& rm -rf /var/lib/apt/lists/*

RUN useradd -d /home/user -u 1000 -m -s /bin/bash user && echo "user ALL= NOPASSWD: ALL" >>/etc/sudoers

USER user
