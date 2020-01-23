FROM ubuntu:20.04

MAINTAINER "https://github.com/best7766"

RUN echo exit 0 > /usr/sbin/policy-rc.d
RUN chmod +x /usr/sbin/policy-rc.d

ENV DEBIAN_FRONTEND noninteractive

RUN cd /root && \
    sed -i 's/^#\s*\(deb.*partner\)$/\1/g' /etc/apt/sources.list && \
    apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y wget && \
    apt-get install -y apt-utils && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:ubuntu-mozilla-daily/ppa && \
    apt-get update -y && \
    apt-get install -yqq locales  && \ 
    echo 'LANG="en_US.UTF-8"' > /etc/default/locale && \ 
    echo 'LANGUAGE="en_US:en"' >> /etc/default/locale && \ 
    echo 'LC_ALL="en_US.UTF-8"' >> /etc/default/locale && \ 
    locale-gen en_US.UTF-8 && \ 
    update-locale LANG=en_US.UTF-8

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
ENV LANG C.UTF-8

RUN apt-get install -y openssh-server
RUN echo 'root:root' |chpasswd
RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
RUN mkdir /root/.ssh

RUN apt-get -y --no-install-recommends install ffmpeg xfce4 xfce4-goodies xorg dbus-x11 x11-xserver-utils

RUN apt-get install --no-install-recommends -yqq \
        firefox \
        preload \
        gnome-system-monitor \
        screenfetch \
        xrdp \
        xorgxrdp \
        supervisor \
        sudo \
        tzdata \
        vim \
        mc \
        ca-certificates \
        curl \
        wget \
        nano \
        git \
        dirmngr \
        net-tools


RUN ln -fs /usr/share/zoneinfo/Europe/London /etc/localtime && dpkg-reconfigure -f noninteractive tzdata && \
    apt-get -y autoclean && apt-get -y autoremove && \
    apt-get -y purge $(dpkg --get-selections | grep deinstall | sed s/deinstall//g) && \
    rm -rf /var/lib/apt/lists/*  && \
    echo "exec startxfce4" >> /etc/xrdp/xrdp.ini && \
    echo "screenfetch" >> /etc/bash.bashrc && \
    echo "2" | update-alternatives --config x-terminal-emulator
    
RUN service xrdp restart

EXPOSE 3389 22
CMD    ["/usr/sbin/sshd", "-D"]
