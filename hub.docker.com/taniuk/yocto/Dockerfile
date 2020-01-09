FROM ubuntu:16.04

LABEL maintainer "tani_k <kazuki@higashitani.org>"

RUN apt-get update \
    && apt-get install -y \
        gawk \
        wget \
        git-core \
        diffstat \
        unzip \
        texinfo \
        gcc-multilib \
        build-essential \
        chrpath \
        socat \
        cpio \
        python \
        python3 \
        python3-pip \
        python3-pexpect \
        xz-utils \
        debianutils \
        iputils-ping \
        libsdl1.2-dev \
        xterm \
        locales \
        vim-nox \
        openssh-server \
    && apt-get clean

RUN mkdir /var/run/sshd

RUN adduser yocto && echo "yocto:yocto" | chpasswd && gpasswd -a yocto sudo
RUN mkdir -p /home/yocto/.ssh; chown yocto /home/yocto/.ssh; chmod 700 /home/yocto/.ssh

WORKDIR /home/yocto

ADD .vimrc /home/yocto
RUN chown yocto:yocto /home/yocto/.vimrc

RUN git clone -b rocko git://git.yoctoproject.org/poky; chown yocto:yocto /home/yocto/poky; chmod -R 775 /home/yocto/poky; mkdir build

RUN locale-gen en_US.UTF-8  
ENV LANG en_US.UTF-8 

EXPOSE 22

CMD /usr/sbin/sshd -D && tail -f /dev/null
